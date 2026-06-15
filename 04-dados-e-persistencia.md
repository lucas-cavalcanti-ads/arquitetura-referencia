# 04 — Dados e Persistência

> **Propósito:** definir como dados são armazenados e como o ambiente de persistência é provisionado, garantindo que tudo rode também localmente.
> **Como a IA deve usar:** ao precisar de banco ou serviços AWS de dados, seguir a abordagem local/nuvem definida aqui.

---

## SGBD

- **PostgreSQL** como banco padrão (transição direta para RDS/Aurora na AWS).

## Migrations

- **Flyway** (SQL-first, integração nativa com Spring Boot). Migrations versionadas no repositório.

## Ambiente local vs. nuvem

Todo sistema **deve rodar localmente** (princípio global). Para isso:

- **Banco local:** **PostgreSQL em container Docker** (via `docker-compose`), na **mesma major version** do RDS. Optou-se por container direto em vez do RDS emulado do LocalStack porque é mais simples, gratuito e integra com Testcontainers.
- **Serviços AWS locais** (S3, SQS, Lambda, etc.): **LocalStack** (edição community, gratuita) para emular a AWS na máquina. Mais barato e leve do que provisionar recursos reais para desenvolvimento.
- **Testes de integração:** Testcontainers sobe o Postgres real (ver `03-qualidade-e-testes.md`).
- **Nuvem:** RDS PostgreSQL provisionado via Terraform (ver `07-infraestrutura-e-ambientes.md`).

> Regra prática: o código aponta para Postgres/serviços AWS via configuração; localmente resolve para o container/LocalStack, na nuvem para RDS/AWS real. A aplicação não muda — só a configuração de ambiente.

## Decisões em aberto

> Nenhuma no momento.
