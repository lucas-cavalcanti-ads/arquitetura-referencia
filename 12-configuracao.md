# 12 — Configuração

> **Propósito:** definir como a aplicação é configurada por ambiente.
> **Como a IA deve usar:** nunca embutir configuração no código; externalizar via ambiente.

---

## Princípios (12-factor)

- **Configuração vem do ambiente**, não do código. Nada de valores de ambiente hardcoded.
- A mesma imagem/artefato roda em qualquer ambiente; só a configuração muda.

## Spring Boot

- Usar **Spring Profiles** para separar contextos — ex.: `local` (LocalStack) e `aws` (serviços reais).
- Endpoints/credenciais resolvidos por perfil: localmente o **endpoint do DynamoDB** aponta para o LocalStack; na nuvem, para o DynamoDB real (ver `04-dados-e-persistencia.md` e `07-infraestrutura-e-ambientes.md`).

## Segredos

- Configuração **sensível** segue as regras de `09-seguranca-e-segredos.md` (Secrets Manager/SSM na AWS, `.env` fora do Git localmente). Config não-sensível pode ficar em `application.yml`/variável de ambiente.

## Documentação

- Toda variável de ambiente documentada no **README** (seção de variáveis — ver `08-governanca-e-documentacao.md`).

## Decisões em aberto

> Nenhuma no momento.
