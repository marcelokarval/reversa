# [Nome do Domínio/Sistema] - Modelo de Domínio e Regras de Negócio

> Template canônico do arquivo `domain.md`. Produzido pelo `reversa-detective` e enriquecido transversalmente.

## 1. Visão Geral do Domínio
[Descrição de alto nível do problema de negócio que o sistema resolve, entidades centrais e limites de contexto / Bounded Contexts].

## 2. Glossário de Termos Ubíquos (Linguagem Ubíqua)

| Termo | Significado no Negócio | Sinônimos / Termos no Código | Confiança |
|-------|------------------------|------------------------------|-----------|
| [ex: Assinatura Ativa] | Cliente com plano pago vigente e sem pendências financeiras | `Subscription.status == 'active'` | 🟢 |
| [ex: Conta em Onboarding] | Usuário cadastrado que ainda não completou os fatos mandatórios | `AccountOnboarding.status == 'required'` | 🟢 |

## 3. Entidades e Agregados Principais
- **[Entidade A]**: Papel no domínio, identificador único, invariantes internas.
- **[Entidade B]**: Papel no domínio, ciclo de vida e relacionamentos.

---

## 4. Invariantes de Negócio Canônicas (Stack-Agnostic)

> **Invariante**: Uma condição ou regra que DEVE permanecer estritamente verdadeira em qualquer estado válido do sistema, independente da linguagem, framework ou banco de dados utilizado.

### 4.1 Invariantes de Identidade e Segurança (Security & Admission)
- **INV-SEC-01**: [Regra estrita, ex: "O identificador primário de autenticação é o e-mail canônico normalizado (trim + lowercase); aliases ou variações não podem causar colisão de identidade."] 🟢
- **INV-SEC-02**: [Regra estrita, ex: "Desafios de autenticação (OTP/Magic Link) são de uso único (One-Time), possuem TTL restrito e invalidam tentativas anteriores abertas."] 🟢

### 4.2 Invariantes de Ciclo de Vida e Estado (Lifecycle & State Invariants)
- **INV-LIFE-01**: [Regra estrita, ex: "Política Fail-Closed: Nenhum ator tem acesso a recursos de domínio protegidos sem a consumação sequencial de todos os fatos de onboarding."] 🟢
- **INV-LIFE-02**: [Regra estrita de transição, ex: "Um estágio de ciclo de vida N só pode ser avaliado e transitado se os fatos mandatórios do estágio N-1 estiverem persistidos."] 🟢

### 4.3 Invariantes de Conformidade e Legalidade (Compliance & Audit)
- **INV-LEG-01**: [Regra estrita, ex: "Consentimento de termos legais é vinculado ao hash criptográfico exato do documento vigente (`content_hash`); alteração de termos invalida consentimentos anteriores e reabre o estágio legal."] 🟢

### 4.4 Invariantes Transacionais e de Concorrência (Data & Resilience)
- **INV-TX-01**: [Regra estrita, ex: "Criação de identidade do usuário deve ser atômica com a inicialização do seu perfil e registro de ciclo de vida correspondente."] 🟢
- **INV-TX-02**: [Regra estrita, ex: "Eventos assíncronos críticos (webhooks de pagamento) devem ser idempotentes e roteados para Dead Letter Queue (DLQ) em caso de falha não recuperável, sem requeue infinito."] 🟢

---

## 5. Regras de Negócio Operacionais

| ID | Regra | Evidência no Código | Confiança |
|----|-------|---------------------|-----------|
| RN-01 | [Descrição da regra operacional] | `caminho/arquivo.ext:linha` | 🟢 |
| RN-02 | [Descrição da regra operacional com suposição] | `caminho/arquivo.ext:linha` | 🟡 |
| RN-03 | [Comportamento observado mas intenção incerta] | `caminho/arquivo.ext:linha` | 🔴 |

## 6. Lacunas e Decisões de Domínio Pendentes
- 🔴 [Lacuna identificada no código que precisa de decisão de negócio humana]
