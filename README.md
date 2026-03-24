Documentação Técnica: Projeto Clone Moodle (LMS)

Este documento detalha a análise completa para o desenvolvimento de um sistema de gestão de aprendizagem (Learning Management System), focado em usabilidade, performance e escalabilidade.

1. Introdução

Este projeto visa o desenvolvimento de um LMS moderno, inspirado nas funcionalidades principais do Moodle. O foco está em criar uma experiência fluida tanto para quem ensina quanto para quem aprende, utilizando padrões de design atuais e uma arquitetura robusta.

1.1 Objetivos

Prover uma plataforma centralizada para cursos online e treinamentos corporativos.

Facilitar a gestão de materiais didáticos (vídeos, PDFs, textos) e avaliações.

Permitir o acompanhamento detalhado do progresso dos alunos e emissão automática de certificados.

1.2 Público-Alvo

Empresas de treinamento: Foco em conformidade e NRs (Segurança do Trabalho).

Instituições de ensino: Escolas e professores autônomos.

Gestores de RH: Treinamentos internos e integração de novos colaboradores (onboarding).

2. Visão Geral do Projeto

O sistema é estruturado de forma modular para permitir a gestão de alunos, instrutores e conteúdos de forma independente.

2.1 Papéis do Sistema (Roles)

Administrador: Gestão global do sistema, criação de categorias de cursos e controle total de usuários.

Professor (Instrutor): Gestão de conteúdos, criação de cursos, acompanhamento de notas e monitorização de alunos.

Aluno: Inscrição e consumo de conteúdos, realização de testes e obtenção de certificados.

3. Requisitos do Sistema

3.1 Requisitos Funcionais (RF)

ID

Requisito

Descrição

Prioridade

RF01

Autenticação

Sistema de Login, Registro e Recuperação de Senha com perfis distintos.

Alta

RF02

Gestão de Cursos

Interface para o professor criar, editar e apagar cursos e categorias.

Alta

RF03

Estrutura Modular

Organização do curso dividida em Módulos e Lições (Aulas).

Alta

RF04

Formatos de Aula

Suporte para Vídeo (Embed), Documentos (PDF) e Texto (Markdown).

Alta

RF05

Matrículas

Inscrição de alunos em cursos (Gratuitos, Pagos ou via Chave).

Alta

RF06

Controle de Progresso

Marcação automática de aula assistida e progresso percentual.

Média

RF07

Avaliações

Criação de Quizzes (Questionários) com correção e nota automática.

Média

RF08

Certificação

Geração automática de certificados em PDF após 100% de conclusão.

Média

RF09

Fórum/Interação

Espaço para comentários e dúvidas em cada aula ou módulo.

Baixa

3.2 Requisitos Não Funcionais (RNF)

ID

Requisito

Descrição

RNF01

Responsividade

A interface deve ser Mobile-First, adaptável a smartphones e tablets.

RNF02

Segurança

Criptografia de senhas (BCrypt) e proteção contra ataques CSRF e XSS.

RNF03

Performance

Otimização de consultas para carregamento de aulas em menos de 2 segundos.

RNF04

Escalabilidade

Arquitetura preparada para suportar múltiplos acessos simultâneos (Stateless).

4. Modelo de Dados (Arquitetura)

Entidades Principais

Utilizador (User): id, nome, email, password_hash, role, data_registo

Curso (Course): id, titulo, descricao, capa_url, professor_id, categoria_id

Módulo (Module): id, curso_id, titulo, ordem

Aula (Lesson): id, modulo_id, titulo, conteudo, tipo, url_media, ordem

Matrícula (Enrollment): id, aluno_id, curso_id, progresso_percentual, data_inicio

5. Diagramas de Fluxo (Mermaid)

5.1 Fluxo de Criação de Conteúdo (Visão Professor)

Este fluxo descreve os passos desde a ideia inicial até a publicação do curso para os alunos.

graph TD
    Start([Início: Painel do Professor]) --> Create[Criar Novo Curso]
    Create --> Details[Definir Título, Capa e Descrição]
    Details --> AddModule[Adicionar Módulo]
    AddModule --> AddLesson[Adicionar Aula ao Módulo]
    AddLesson --> Type{Tipo de Conteúdo?}
    Type -- Vídeo --> Video[Inserir Link YouTube/Vimeo]
    Type -- Arquivo --> File[Upload de PDF/Docs]
    Type -- Texto --> Text[Escrever Conteúdo no Editor]
    Video & File & Text --> More{Mais Aulas?}
    More -- Sim --> AddLesson
    More -- Não --> Review[Revisar Curso]
    Review --> Publish[Publicar Curso para Alunos]
    Publish --> End([Fim: Curso Online])


5.2 Experiência do Aluno e Progresso

Garante que a jornada do aluno seja registrada e recompensada.

sequenceDiagram
    participant A as Aluno
    participant S as Sistema
    participant DB as Banco de Dados

    A->>S: Acessa a Aula X
    S->>DB: Busca conteúdo e mídia da Aula X
    DB-->>S: Retorna Dados (Vídeo/PDF)
    S-->>A: Exibe interface de Aula
    A->>S: Clica em "Marcar como Concluída"
    S->>DB: Atualiza progresso na tabela Enrollment
    S->>DB: Verifica se todas as aulas foram concluídas
    DB-->>S: Resposta: Concluído (Sim/Não)
    alt É a última aula?
        S-->>A: Notifica Conclusão e Gera Certificado PDF
    else Ainda faltam aulas
        S-->>A: Libera acesso à próxima aula da sequência
    end


6. Regras de Negócio (RN)

RN01 - Acesso Restrito: O conteúdo das aulas só é visível para usuários com uma matrícula (Enrollment) ativa para aquele curso específico.

RN02 - Integridade do Progresso: Uma aula marcada como "Concluída" não deve retornar ao estado inicial automaticamente, a menos que o aluno opte por reiniciar o progresso (se permitido).

RN03 - Certificação: O certificado de conclusão só é emitido se o campo progresso_percentual da matrícula for igual a 100.

RN04 - Permissões de Edição: Apenas o autor original do curso (Professor) ou um Administrador do sistema podem alterar materiais didáticos após a publicação.

7. Mapa do Site (Navegação)

Público: * Home (Lançamentos e Destaques)

Catálogo de Cursos (Busca e Categorias)

Páginas de Login/Registro

Área do Aluno: * Dashboard (Meus Cursos em andamento)

Sala de Aula Virtual (Player de vídeo e materiais)

Página de Certificados

Área do Professor: * Painel de Instrutor (Estatísticas de vendas/alunos)

Gerenciador de Cursos (Criação de módulos e aulas)

Relatórios de Desempenho

Painel Administrativo: * Gestão de Usuários (Banir/Promover)

Configurações Gerais de Sistema e Branding
