# 04 — Dados e Persistência

> **Propósito:** definir como dados são armazenados e como o ambiente de persistência é provisionado, garantindo que tudo rode também localmente.
> **Como a IA deve usar:** ao precisar de banco, usar DynamoDB conforme as regras abaixo. Garantir sempre o funcionamento local.

---

## Banco de dados

- **Amazon DynamoDB** é o banco de dados padrão.
- **Modo de capacidade: on-demand (pay-per-request).** Sempre trabalhar com o **menor recurso possível sob demanda** — sem capacidade provisionada, paga-se por requisição.
- Evitar desperdício de recurso: criar apenas os índices realmente necessários (cada GSI tem custo), manter os itens enxutos e modelar pelos padrões de acesso.

## Modelagem

- Modelagem **orientada aos padrões de acesso** (access-pattern-driven), não ao modelo relacional.
- Definir chave de partição (e de ordenação, quando necessário) a partir das consultas que a aplicação precisa fazer.
- Índices secundários (GSI/LSI) só quando um padrão de acesso exigir — manter ao mínimo.

## Estrutura de tabelas e "migrations"

- DynamoDB não tem esquema fixo de colunas. **Definição de tabelas e índices é feita via Terraform** (IaC — ver `07-infraestrutura-e-ambientes.md`), nunca no console.
- Mudanças estruturais (nova tabela, novo GSI) entram como alteração de Terraform.
- Backfill/transformação de dados, quando necessário, via **scripts versionados** no repositório.

## Acesso ao banco

- **Java:** AWS SDK for Java v2 com **DynamoDB Enhanced Client**.
- **Lambdas Python:** `boto3`.

## Ambiente local vs. nuvem

Todo sistema **deve rodar localmente** (princípio global). Para isso:

- **Local:** **LocalStack** emula o DynamoDB na máquina (via `docker-compose`). A mesma definição de tabela usada na AWS é aplicada no LocalStack.
- **Nuvem:** DynamoDB real, on-demand, provisionado via Terraform.
- O código aponta para o DynamoDB via configuração (endpoint): localmente resolve para o LocalStack; na nuvem, para o serviço real (ver `12-configuracao.md`). A aplicação não muda — só a configuração de ambiente.

## Testes

- **Testes de integração** rodam contra o DynamoDB do **LocalStack** (ex.: Testcontainers com o módulo LocalStack), sem mocar o banco — ver `03-qualidade-e-testes.md`.

## Decisões em aberto

> Nenhuma no momento.
