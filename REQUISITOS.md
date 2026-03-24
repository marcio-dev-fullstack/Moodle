# Documento de Requisitos

## 1. Requisitos Funcionais (RF)

| ID | Requisito | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF01 | Gestão de Usuários | Cadastro, login e recuperação de senha. | Alta |
| RF02 | Níveis de Acesso | Perfis diferenciados: Admin, Professor e Aluno. | Alta |
| RF03 | Criação de Cursos | Interface para o professor criar cursos e categorias. | Alta |
| RF04 | Estrutura de Módulos | Divisão de conteúdos por tópicos ou semanas. | Alta |
| RF05 | Upload de Materiais | Suporte a PDF, Imagens e Vídeos (Embed). | Alta |
| RF06 | Sistema de Matrícula | Inscrição manual ou automática em cursos. | Média |
| RF07 | Fórum de Dúvidas | Espaço de interação em cada aula. | Baixa |
| RF08 | Avaliações (Quizzes) | Criação de testes de múltipla escolha. | Média |
| RF09 | Emissão de Certificado | Geração automática de PDF após conclusão. | Média |

## 2. Requisitos Não Funcionais (RNF)

| ID | Requisito | Descrição |
| :--- | :--- | :--- |
| RNF01 | Segurança | Criptografia de senhas e proteção CSRF/XSS. |
| RNF02 | Responsividade | Interface adaptável para Mobile e Desktop. |
| RNF03 | Desempenho | Tempo de resposta de APIs abaixo de 200ms. |
| RNF04 | Escalabilidade | Arquitetura pronta para rodar em containers (Docker). |
