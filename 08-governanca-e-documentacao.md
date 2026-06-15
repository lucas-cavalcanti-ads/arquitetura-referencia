# 08 — Governança e Documentação

> **Propósito:** definir regras de documentação e restrições globais que valem para todos os artefatos.
> **Como a IA deve usar:** estas regras são transversais e se aplicam a qualquer entrega. Em especial, a restrição de idioma vale para tudo.

---

## Documentação no repositório

- Toda aplicação deve ser documentada de forma **técnica e funcional** no **`README` na raiz do repositório**.
- Regra de manutenção:
  - Se o `README` **já existe** → deve ser **atualizado** para refletir o estado atual.
  - Se **não existe** → deve ser **criado e preenchido**.
- O `README` é entregável de primeira classe: nenhuma feature está pronta sem a documentação correspondente atualizada.

### Seções padrão do README

1. **Visão funcional** — o que a aplicação faz, qual problema resolve, principais fluxos de negócio.
2. **Arquitetura** — visão técnica, camadas, decisões principais.
3. **Como rodar localmente** — `docker-compose` (LocalStack + banco), pré-requisitos, variáveis.
4. **Testes e CI** — como rodar testes e o que a pipeline valida.
5. **Deploy** — como o sistema vai para a AWS.
6. **Variáveis de ambiente** — lista e descrição.

## ADRs (Architecture Decision Records)

- Decisões arquiteturais relevantes registradas em `docs/adr/` (um arquivo por decisão).

## Mensagens de commit

- **Conventional Commits** (amarra com o versionamento SemVer do CI — ver `06-ci-cd-e-deploy.md`).

## Documentação de API

- Quando houver REST (Spring Boot), gerar documentação **OpenAPI/Swagger**.

## Restrição de idioma (global)

- **Todos os artefatos devem ser escritos em Português (Brasil).**
- Inclui: documentação, README, comentários de código, mensagens de log, identificadores de log, mensagens de commit, corpo de PR e qualquer texto gerado.

## Decisões em aberto

> Nenhuma no momento.
