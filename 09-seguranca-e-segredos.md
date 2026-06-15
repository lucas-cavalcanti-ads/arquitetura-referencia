# 09 — Segurança e Segredos

> **Propósito:** regras mínimas de segurança, com foco em não vazar credencial.
> **Como a IA deve usar:** nunca colocar segredo em código ou artefato versionado. Seguir as fontes de segredo por ambiente.
> **Escopo:** intencionalmente enxuto.

---

## Segredos (regra principal)

- **Segredo nunca vai para o repositório** — nem em código, config versionada, log ou corpo de PR.
- Fontes de segredo por ambiente:
  - **Local:** variável de ambiente ou arquivo `.env` **fora do Git** (`.env` no `.gitignore`).
  - **Nuvem (AWS):** **AWS Secrets Manager** ou **SSM Parameter Store**.
  - **CI/CD:** **GitHub Actions Secrets**.
- `.gitignore` deve cobrir `.env`, chaves e arquivos de credencial.
- **Credencial exposta = rotacionar imediatamente** (revogar e gerar nova).

## Autenticação/autorização

- Quando houver API REST que exija auth: **Spring Security com OAuth2/JWT**.
- Não reinventar autenticação; usar o que o Spring Security oferece.

## Dependências

- **Dependabot** ativo (alinha com o scan já previsto no CI — ver `06-ci-cd-e-deploy.md`).

## Transporte

- Comunicação externa sempre sobre **TLS/HTTPS**.

## Decisões em aberto

> Nenhuma no momento. Expandir só se um projeto específico exigir (ex.: requisitos regulatórios mais fortes).
