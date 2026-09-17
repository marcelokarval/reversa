# Especificação de Software e Design (SDD)

## Missão e Objetivo
Esta especificação contém a documentação executável gerada por engenharia reversa do sistema legado. O objetivo é fornecer a base contratual, arquitetural e comportamental exata para reconstrução, refatoração ou entendimento da plataforma, com zero ambiguidade técnica.

## Topologia de Artefatos

O repositório de specs está organizado em pastas por unidades lógicas (módulos, casos de uso ou endpoints). Cada unidade contém os seguintes artefatos canônicos:

* **`requirements.md` (O QUE):** Critérios de aceite, requisitos não-funcionais (performance, segurança) e Invariantes de Domínio.
* **`design.md` (COMO):** Modelagem de dados, arquitetura interna, dependências, fluxos e tratamento de erros.
* **`tasks.md` (PLANO):** Breakdown técnico de tarefas com Definition of Done.
* **`domain.md` (REGRAS/INVARIANTES):** (se aplicável) Dicionário de domínio, agregação de regras core.

Além disso, a raiz contém:
* `transformation-guide.md`: Playbook de reconstrução arquitetural.
* `openapi/`: Contratos de integração (HTTP/Webhooks).
* `traceability/code-spec-matrix.md`: Matriz de cobertura.

## Protocolo de Ingestão (5 Passos)

Para que LLMs e desenvolvedores processem estas specs com máxima eficiência na hora da implementação:

1. **Contexto Raiz:** Leia este `README.md` e o `transformation-guide.md` para entender as regras do jogo.
2. **Contratos:** (Se existirem integrações) Leia `openapi/<unit>.yaml`.
3. **Requisitos da Unidade:** Leia `<unit>/requirements.md` com foco nas **Invariantes (INV-*)**.
4. **Design Interno:** Leia `<unit>/design.md` para mapear de onde os dados vêm e como a lógica orquestra.
5. **Execução:** Siga o plano de ação estrito contido em `<unit>/tasks.md`.

## Glossário de Termos
*(Preencha os termos críticos de negócio e jargões do projeto)*
* **Unit:** Unidade mínima de valor mapeada pelo Reversa (pode ser módulo, use-case, feature).
* **SDD:** Software Design Document.
* **INV-XX:** Invariante de Domínio. Regras de negócio essenciais e inegociáveis.

## Índice de Units

*(O índice será preenchido automaticamente pela IA com a lista das units geradas)*
