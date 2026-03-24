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
