# Technical Improvement Specification (SDD)

This document defines a **Specification-Driven Development (SDD)** plan for the future evolution of the `golang-microsservice-with-rabbitmq` ecosystem.

Este documento define um plano de **Specification-Driven Development (SDD)** para a evolução futura do ecossistema `golang-microsservice-with-rabbitmq`.

The goal is to transform the current technical debt analysis into an executable specification that can guide refactoring, modernization, documentation, and infrastructure improvements over time.

O objetivo é transformar a análise de dívida técnica atual em uma especificação executável que possa orientar refatorações, modernização, documentação e melhorias de infraestrutura ao longo do tempo.

---

## 1. Scope | Escopo

This specification covers the following repositories and components:

Esta especificação cobre os seguintes repositórios e componentes:

- `peacevan/golang-microsservice-with-rabbitmq`
- `peacevan/microsservice-ecommerce`
- `peacevan/microsservice-ecommerce-admin`
- local infrastructure defined through Docker and RabbitMQ
- local development and execution documentation
- asynchronous communication contracts between services

### Out of Scope | Fora do Escopo

- creation of new business features unrelated to technical improvement
- migration to a different programming language
- replacing RabbitMQ with another broker in this phase
- full production platform redesign

---

## 2. Background | Contexto

The current project demonstrates a Go-based microservices architecture using RabbitMQ and PostgreSQL, with the root repository acting as an entry point for documentation, shared setup, and Git submodule orchestration.

At the same time, the codebase shows signs of accumulated technical debt, including naming inconsistencies, legacy dependency versions, possible template leftovers, weak default local credentials, duplicated configuration patterns, and missing automation for code quality.

O projeto atual demonstra uma arquitetura de microsserviços em Go utilizando RabbitMQ e PostgreSQL, com o repositório raiz atuando como ponto de entrada para documentação, setup compartilhado e orquestração via Git submodules.

Ao mesmo tempo, a base de código apresenta sinais de dívida técnica acumulada, incluindo inconsistências de nomenclatura, versões legadas de dependências, possíveis resíduos de templates anteriores, credenciais locais fracas por padrão, padrões duplicados de configuração e ausência de automação para qualidade de código.

---

## 3. Objectives | Objetivos

### Primary Objectives | Objetivos Primários

- align repository and code naming with the actual e-commerce domain
- improve maintainability and onboarding experience
- modernize dependencies and infrastructure safely
- strengthen local-development security defaults
- document service responsibilities and messaging contracts clearly
- create a structured roadmap for incremental technical improvement

### Secondary Objectives | Objetivos Secundários

- reduce ambiguity between the root repository and service submodules
- improve developer experience through automation and standard commands
- create a future-ready baseline for CI/CD and observability

---

## 4. Problem Statements | Declaração dos Problemas

### 4.1 Domain naming inconsistency
Observed examples suggest that parts of the codebase still reference names inherited from a previous template or unrelated project, such as `encoder` and `cryptosharing`.

**Impact:**
- reduces clarity
- harms onboarding
- makes the project appear unfinished
- increases the chance of environment misconfiguration

### 4.2 Outdated or legacy technical stack
The project currently uses old Go, PostgreSQL, and library versions.

**Impact:**
- higher maintenance cost
- lower compatibility with current tooling
- higher long-term security and upgrade risk

### 4.3 Insecure or weak local defaults
Default credentials and fixed environment values appear in local configuration.

**Impact:**
- encourages insecure habits
- increases accidental misuse across environments
- makes production-hardening harder later

### 4.4 Docker and build process misalignment
The current container setup appears to include tooling that may not belong to the e-commerce domain, and production images may include local runtime artifacts.

**Impact:**
- larger images
- wider attack surface
- harder maintenance
- potential secret leakage risk

### 4.5 Missing quality automation
There is no documented evidence of CI, linting, structured verification, or standardized developer workflows across repositories.

**Impact:**
- inconsistent code quality
- slower feedback loops
- higher regression risk

### 4.6 Underspecified asynchronous contracts
RabbitMQ queues, exchanges, routing keys, and payload expectations are only partially implicit in environment files and code structure.

**Impact:**
- weak interoperability guarantees
- higher integration risk
- harder troubleshooting

---

## 5. Guiding Principles | Princípios Norteadores

- **Incremental change first**: prefer safe and staged evolution over large rewrites.
- **Documentation follows reality**: specs must reflect implementation truth.
- **Security by default**: local convenience must not normalize insecure production practices.
- **Explicit contracts**: service boundaries and event flows must be clearly described.
- **Automation over convention**: repeated manual checks should become automated.
- **Keep the project teachable**: preserve educational value while increasing professionalism.

---

## 6. Functional Areas and Requirements | Áreas Funcionais e Requisitos

## 6.1 Project Identity and Naming

### Requirements
- Replace legacy names that do not reflect the domain.
- Standardize repository, service, database, queue, and module naming.
- Decide whether `microsservice` should be kept for backward compatibility or renamed to `microservice`.

### Acceptance Criteria
- No template leftovers remain in user-facing configuration or documentation.
- Naming conventions are documented.
- The chosen naming standard is applied consistently.

---

## 6.2 Documentation and Developer Onboarding

### Requirements
- Keep the root README aligned with actual setup and architecture.
- Improve service-level READMEs in each submodule.
- Document how to start the full local environment.
- Document all required environment variables.
- Document event flow and RabbitMQ topology.

### Acceptance Criteria
- A new contributor can clone the project and understand the setup path without external explanation.
- Root repository and submodule responsibilities are clearly separated.
- Event communication is understandable from documentation alone.

---

## 6.3 Configuration Management

### Requirements
- Review `.env.example` files in all services.
- Group variables by concern: app, database, messaging, debug, test.
- Validate required variables at startup.
- Differentiate dev/test/prod configuration strategy.

### Acceptance Criteria
- Missing required variables cause immediate and explicit startup failure.
- `.env.example` files reflect real service needs.
- Environment configuration is documented and reproducible.

---

## 6.4 Security Hardening

### Requirements
- Remove weak or misleading default credentials where possible.
- Avoid embedding runtime secrets in Docker images.
- Replace fixed secrets with runtime-provided values for non-development environments.
- Review local defaults and document that they are development-only.

### Acceptance Criteria
- Production images do not include `.env` or secret files.
- Sensitive configuration is injected at runtime.
- Security-sensitive defaults are clearly documented and isolated.

---

## 6.5 Docker and Infrastructure Modernization

### Requirements
- Review Dockerfiles for unnecessary packages and inherited tooling.
- Reassess the need for `ffmpeg` and `Bento4` in the current domain.
- Reduce image complexity and size.
- Clarify the role of root-level vs service-level Docker Compose files.

### Acceptance Criteria
- Docker images include only required runtime dependencies.
- Compose strategy is documented and not duplicated ambiguously.
- Build steps match the real application domain.

---

## 6.6 Dependency and Runtime Modernization

### Requirements
- Plan safe upgrades for Go, PostgreSQL, Docker base images, and Go libraries.
- Review legacy dependencies and identify migration paths.
- Evaluate migration from legacy GORM package to modern maintained package.

### Acceptance Criteria
- A version-upgrade roadmap exists before implementation begins.
- Breaking changes are explicitly identified.
- Dependencies are justified and current enough for maintainable development.

---

## 6.7 Code Quality and Automation

### Requirements
- Standardize formatting, linting, and vetting.
- Expand Makefile or task runner commands.
- Add CI validation for build, tests, formatting, and linting.

### Acceptance Criteria
- A standard local developer workflow exists.
- CI provides automated feedback on pull requests.
- Formatting and static checks are reproducible.

---

## 6.8 Testing Strategy

### Requirements
- Separate unit and integration test concerns.
- Add coverage for messaging flows and persistence behavior.
- Define mocking or test-container strategy for RabbitMQ and database interactions.

### Acceptance Criteria
- Critical flows are testable without manual steps.
- Integration behavior is validated intentionally.
- Test intent is documented.

---

## 6.9 Observability and Diagnostics

### Requirements
- Standardize structured logs.
- Improve visibility of publish/consume event operations.
- Add health and readiness checks where applicable.

### Acceptance Criteria
- Operational failures are easier to diagnose.
- Service startup and integration state are explicit.
- Logs support cross-service troubleshooting.

---

## 6.10 Messaging Contracts

### Requirements
- Define queue, exchange, routing key, and dead-letter semantics.
- Document payload shape and compatibility expectations.
- Define retry and idempotency expectations for consumers.

### Acceptance Criteria
- Service integration behavior is documented as a contract.
- Payload expectations are explicit.
- Failure-handling strategy is documented.

---

## 7. Proposed Execution Phases | Fases Propostas de Execução

### Phase 1 — Foundation Cleanup | Fase 1 — Limpeza de Fundação
- correct naming inconsistencies
- review service READMEs
- clean `.env.example` files
- remove obvious template leftovers
- review Dockerfiles for secrets and domain mismatch

### Phase 2 — Modernization | Fase 2 — Modernização
- upgrade Go and base images
- review PostgreSQL version strategy
- audit and upgrade dependencies
- prepare migration plan for legacy packages

### Phase 3 — Quality and Automation | Fase 3 — Qualidade e Automação
- add linting and vetting
- improve Makefiles
- add CI workflows
- improve test coverage strategy

### Phase 4 — Reliability and Contracts | Fase 4 — Confiabilidade e Contratos
- document messaging contracts
- add health/readiness checks
- standardize logs and diagnostics
- improve observability practices

---

## 8. Risks | Riscos

- renaming repositories, modules, or services may break links, imports, or local workflows
- dependency upgrades may require code refactoring
- standardizing event contracts may reveal hidden coupling
- submodule synchronization may become more complex during transition

### Mitigation Strategies | Estratégias de Mitigação
- perform changes incrementally
- separate documentation updates from runtime changes where possible
- validate each phase independently
- avoid multi-dimensional refactors in a single step

---

## 9. Deliverables | Entregáveis

The future implementation guided by this specification should produce:

- updated and aligned documentation
- cleaner configuration files
- safer Docker and environment practices
- dependency modernization plan and execution
- CI and quality automation
- explicit RabbitMQ integration contracts
- clearer service ownership boundaries

---

## 10. Definition of Done | Definição de Pronto

This specification is considered fulfilled when:

- naming is domain-consistent
- local setup is documented and reproducible
- service responsibilities are clear
- secret handling follows safer patterns
- containers are aligned with actual application needs
- code quality checks are automated
- integration contracts are explicitly documented
- technical debt identified in this document is either resolved or formally deferred with rationale

---

## 11. Suggested Future Specs | Especificações Futuras Sugeridas

To make execution easier, this master specification can later be split into smaller implementation specs:

- `specs/01-project-naming-and-domain-alignment.md`
- `specs/02-config-and-secret-management.md`
- `specs/03-docker-modernization.md`
- `specs/04-runtime-and-dependency-upgrades.md`
- `specs/05-code-quality-and-ci.md`
- `specs/06-rabbitmq-contracts.md`
- `specs/07-testing-strategy.md`

---

## 12. Final Note | Nota Final

This document is intentionally implementation-agnostic. It exists to support future planning, prioritization, and incremental correction using an SDD-style workflow.

Este documento é intencionalmente agnóstico à implementação. Ele existe para apoiar planejamento futuro, priorização e correção incremental usando um fluxo no estilo SDD.
