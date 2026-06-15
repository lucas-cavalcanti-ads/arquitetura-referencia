# 02 — Stacks Tecnológicas

> **Propósito:** registrar linguagens, frameworks, runtimes e versões preferidas.
> **Como a IA deve usar:** ao escolher dependências ou gerar código, priorize esta stack. Não introduza tecnologia fora dela sem sinalizar e justificar.

---

## Linguagens

- **Backend:** Java 21 (LTS).
- **Funções serverless (Lambdas):** Python **3.13** (runtime suportado pela AWS).

## Build e gerenciamento de dependências

- **Java:** Maven.
- **Lambdas Python:** empacotamento feito **pelo próprio Terraform** (módulo `terraform-aws-modules/lambda`), evitando adicionar SAM/Serverless Framework — IaC fica unificada no Terraform.

## Gerenciamento de versões no ambiente

- **Java:** SDKMAN (Java 21 Temurin LTS).
- **Python:** pyenv.

## Frameworks backend

- **Spring Boot** quando o componente expõe **API REST**.
- Para Lambdas em Python, manter o runtime enxuto (evitar framework web pesado; usar o handler nativo da Lambda).

## Observações de uso

- Java 21 + Maven é o default para serviços backend.
- Python fica reservado para Lambdas e automações pontuais.
- Spring Boot entra **quando há API REST**. Para um componente Java sem REST, avaliar se Spring Boot é mesmo necessário.

## Decisões em aberto

> Nenhuma no momento.
