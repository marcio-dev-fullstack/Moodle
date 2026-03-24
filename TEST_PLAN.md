Plano de Testes (Quality Assurance)

Este documento define a estratégia de validação das funcionalidades do sistema.

1. Testes Unitários (Backend)

Foco: Validação de lógica de negócio em Models e Serializers.

Ferramenta: pytest / unittest.

Cobertura Mínima: 80%.

2. Testes de Integração

Fluxo de Matrícula: Validar se a criação de uma Enrollment gera corretamente o acesso aos módulos.

Cálculo de Progresso: Garantir que ao marcar 5 de 10 aulas, o progresso reflete 50%.

3. Testes de Interface (E2E)

Ferramenta: Cypress ou Selenium.

Cenários Críticos:

Login com diferentes perfis (Admin, Professor, Aluno).

Fluxo completo de criação de curso por um Professor.

Realização de um Quiz e verificação de nota.

4. Testes de Carga e Performance

Objetivo: Garantir o carregamento de páginas em menos de 2s com 100 utilizadores simultâneos.

Ferramenta: JMeter ou Locust.

5. Critérios de Aceitação

Uma funcionalidade só é considerada "Concluída" se passar em todos os testes automatizados e for validada manualmente em ambiente de Staging.
