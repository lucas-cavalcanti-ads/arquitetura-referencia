# 07 — Infraestrutura e Ambientes

> **Propósito:** definir como a infraestrutura é provisionada e empacotada.
> **Como a IA deve usar:** ao propor ou gerar infraestrutura, usar as ferramentas definidas aqui e garantir que tudo também rode localmente.

---

## Provedor de nuvem

- **AWS.**

## Provisionamento de infraestrutura

- **Terraform** como ferramenta de Infrastructure as Code.
- Toda infraestrutura de nuvem é descrita como código (versionada), não criada manualmente no console.
- **Ambiente único** — não há separação dev/staging/prod. Mantém a estrutura do Terraform simples (sem múltiplos workspaces ou pastas por ambiente).

> **Nota sobre "estado do Terraform":** o Terraform guarda um arquivo de *state* que registra o que ele já criou na AWS. Por padrão esse arquivo fica local na máquina; se ele se perde ou corrompe, o Terraform "esquece" o que existe. Como há um só ambiente, dá para começar com o state local. Se em algum momento mais de uma pessoa/máquina for aplicar o Terraform, vale migrar o state para um bucket S3 (com lock em DynamoDB) para evitar conflito. _Decisão atual: state local; reavaliar se houver mais de um operador._

## Empacotamento e execução

- **Docker** para empacotar e executar aplicações.
- **Registry de imagens:** Amazon ECR.

## Execução local (princípio global)

- Todo sistema **deve rodar localmente**.
- **LocalStack** emula os serviços AWS na máquina; **Postgres em container** para o banco (ver `04-dados-e-persistencia.md`).
- Ideal: um `docker-compose` que sobe LocalStack + banco + aplicação, permitindo rodar o sistema completo offline.

## Decisões em aberto

> Nenhuma no momento.
