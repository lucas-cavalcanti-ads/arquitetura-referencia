# 03 — Qualidade e Testes

> **Propósito:** definir o padrão de qualidade de código e a estratégia de testes.
> **Como a IA deve usar:** todo código gerado deve vir acompanhado de testes que atendam ao critério de cobertura. Não pular testes por padrão.

---

## Cobertura de testes

- **Cobertura mínima de testes unitários: 95%.**
- O gate de 95% é aplicado **por módulo** (não apenas na média global) — um módulo bem testado não pode mascarar outro sem teste.
- Medir cobertura de **linha + branch**.
- Verificado na pipeline de CI (ver `06-ci-cd-e-deploy.md`); cobertura abaixo do mínimo reprova o CI.

## Ferramentas de teste

- **Java:** JUnit 5 + Mockito + AssertJ; cobertura com **JaCoCo** (build falha abaixo de 95%).
- **Python:** pytest + pytest-cov.

## Estratégia de testes

- Foco forte em **testes unitários** sobre as regras de domínio e os casos de uso (camadas internas da Clean Architecture).
- **Testes de integração com Testcontainers (módulo LocalStack)** — alinhado ao "DynamoDB via LocalStack" (ver `04-dados-e-persistencia.md`): sobe o DynamoDB emulado em container durante os testes, sem mocar o banco.
- Contract testing (Pact / Spring Cloud Contract) só quando houver mais de um serviço se comunicando — não adicionar peso antes disso.

## Critério de "pronto"

- Código com testes.
- Cobertura unitária ≥ 95% por módulo (linha + branch).
- CI verde.

## Decisões em aberto

> Nenhuma no momento.
