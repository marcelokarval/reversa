# Playbook de Reengenharia e Transformação

Este guia estabelece os parâmetros arquiteturais, metodológicos e de ciclo de vida para a reconstrução, migração ou evolução do sistema.

## 1. Princípio Fundamental

**A especificação governa a regra; a linguagem alvo governa a ergonomia técnica.**
As Invariantes de Domínio (`INV-*`) contidas nos arquivos `requirements.md` não podem ser alteradas sem aprovação de negócios. Contudo, a forma como essas regras são implementadas deve seguir os melhores padrões da *nova* stack de tecnologia.

## 2. Metodologia TDD First (Obrigatória)

Todo código novo deve ser orientado a testes antes da codificação lógica.
1. **Invariantes → Testes Unitários:** Cada invariante de domínio (`INV-*`) deve gerar, no mínimo, um teste unitário que valide seu limite.
2. **Critérios de Aceite → BDD/E2E:** Os fluxos descritos (Dado / Quando / Então) nos `requirements.md` devem ser mapeados para testes E2E ou de integração (ex: Cucumber/Gherkin).

## 3. Mapeamento Arquitetural (Hexagonal / Clean Architecture)

Sempre que a aplicação permitir, adote o desacoplamento:
* **Domain (Core):** Onde as entidades e `INV-*` vivem. Sem dependências externas.
* **Use Cases (Application):** Orquestram o fluxo detalhado no `design.md`.
* **Adapters (Portas de Entrada/Saída):**
    * *Inbound:* Controladores HTTP (definidos nos `openapi/*.yaml`), Event Listeners.
    * *Outbound:* Repositórios (SQL/NoSQL), clientes API.

## 4. Matriz de Dependências e Reconstrução Incremental

A reconstrução deve priorizar componentes com o menor número de dependências ativas (Bottom-Up) ou os de maior valor de negócio isolado. Consulte a matriz em `traceability/code-spec-matrix.md` para identificar impactos colaterais.

## 5. Instruções para os Fluxos do Reversa

A integração contínua com a IA do Reversa segue fluxos bem definidos:
* **/reversa-reconstructor:** Utilizado para planejar sprints e epic breakdowns a partir das units documentadas.
* **/reversa-forward:** Ciclo de desenvolvimento TDD; cria as features e seus `legacy-impact.md`.
* **/reversa-code-express:** Usado para refatorações "one-shot" de baixo risco.
* **/reversa-sync:** Sempre execute para converger as mudanças do forward (`_reversa_forward/`) com a base de specs (`_reversa_sdd/`).

## 6. Definition of Done (DoD)

Uma unit reconstruída ou migrada só está "Pronta" quando:
- [ ] 100% das `INV-*` possuem testes de regressão automatizados verdes.
- [ ] O código implementa todos os Critérios de Aceite definidos.
- [ ] Não há "hardcodes" mapeados na versão antiga sem justificativa.
- [ ] Contratos de I/O (`openapi/<unit>.yaml`) foram validados via linter/schemas.
- [ ] A matriz de rastreabilidade do Reversa confirmou a cobertura.