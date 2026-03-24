# Diagramas de Fluxo do Sistema (LMS)

Este documento descreve visualmente os processos principais de interação entre os usuários e a plataforma.

## 1. Fluxo de Autenticação e Autorização
Este fluxo garante que o usuário acesse apenas as áreas permitidas conforme seu perfil.

```mermaid
graph TD
    A[Usuário acessa a Home] --> B{Possui Conta?}
    B -- Não --> C[Realizar Cadastro]
    B -- Sim --> D[Realizar Login]
    C --> D
    D --> E{Qual o Perfil?}
    E -- Aluno --> F[Dashboard do Aluno / Meus Cursos]
    E -- Professor --> G[Painel do Instrutor / Gestão de Cursos]
    E -- Admin --> H[Painel Administrativo Geral]

## 2. Fluxo de Criação de Conteúdo (Visão Professor)

flowchart LR
    P[Professor] --> C[Criar Novo Curso]
    C --> M[Adicionar Módulos]
    M --> L[Adicionar Aulas/Conteúdos]
    L --> V{Tipo de Aula?}
    V -- Vídeo --> V1[Inserir URL Embed]
    V -- PDF --> V2[Fazer Upload do Arquivo]
    V -- Texto --> V3[Escrever no Editor Rich Text]
    V1 & V2 & V3 --> PUB[Publicar Curso]

## 3. Fluxo de Experiência do Aluno (Consumo de Aula)

sequenceDiagram
    participant A as Aluno
    participant S as Sistema/LMS
    participant B as Banco de Dados

    A->>S: Clica em "Iniciar Aula"
    S->>B: Verifica se está matriculado
    B-->>S: Confirma Matrícula
    S-->>A: Exibe Vídeo/PDF
    A->>S: Clica em "Concluir Aula"
    S->>B: Registra progresso (100%)
    S->>B: Verifica se há próxima aula
    B-->>S: Retorna ID da próxima aula
    S-->>A: Libera botão "Próxima Aula"

## 4. Fluxo de Avaliação e Certificação

graph TD
    ST[Início da Avaliação] --> Q[Responder Questionário]
    Q --> SUB[Submeter Respostas]
    SUB --> CALC{Nota >= 70%?}
    CALC -- Não --> RET[Oportunidade de Refazer]
    RET --> Q
    CALC -- Sim --> PROG{Progresso Aulas = 100%?}
    PROG -- Não --> AUL[Finalizar Aulas Restantes]
    PROG -- Sim --> CERT[Gerar Certificado PDF]
    CERT --> END[Fim do Processo]
