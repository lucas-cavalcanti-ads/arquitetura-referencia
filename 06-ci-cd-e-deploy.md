# 06 — CI/CD e Deploy

> **Propósito:** definir pipeline de integração contínua, fluxo de branches e regras de merge.
> **Como a IA deve usar:** ao configurar automação de repositório, seguir este fluxo. Pipelines geradas devem refletir exatamente os gates descritos.

---

## Ferramenta de pipeline

- **GitHub Actions** para CI/CD.

## Fluxo de branches (feature branches → main)

> Fluxo baseado em **feature branches integrando direto na `main`** (estilo GitHub Flow / trunk-based). **Não** é o Git Flow clássico — não há `develop`, `release/*` nem `hotfix/*`.

- **Qualquer branch** dispara a pipeline de **CI com testes** ao receber push.
- O resultado do CI controla a abertura de PR:
  - **CI falhou** → **não abre PR**.
  - **CI passou** → a pipeline **abre automaticamente um PR para a `main`**.
- A branch **`main` é protegida**: só recebe alterações via PR com CI verde.

## Abertura automática de PR com contexto para review

Quando o CI passa em uma branch, a pipeline:

1. **Abre o PR para a `main` automaticamente** (ex.: `gh pr create`).
2. **Analisa as mudanças** (diff + commits) e **preenche o corpo do PR** com informações que facilitam o code review, por exemplo:
   - Resumo do que mudou e por quê.
   - Lista de arquivos/áreas afetadas.
   - Resultado dos gates (testes, cobertura).
   - Pontos de atenção sugeridos para o revisor.

> O resumo pode ser gerado a partir dos Conventional Commits e do diff; opcionalmente enriquecido por um sumarizador automático. Objetivo: o revisor abrir o PR e já ter o contexto pronto.

## Gates obrigatórios no CI

1. **Build** (`mvn verify`).
2. **Lint/format** — Spotless + Checkstyle (Java); **ruff** (Python).
3. **Análise estática** — SpotBugs ou SonarCloud.
4. **Testes** + **cobertura ≥ 95% por módulo** (JaCoCo) — ver `03-qualidade-e-testes.md`. Reprova o CI e impede a abertura de PR.
5. **Scan de segurança** — dependências (Dependabot) e imagem (Trivy).
6. **Build da imagem Docker** → push para **Amazon ECR**.

## Deploy

- Ambiente **único** (efetivamente produtivo).
- Deploy a partir da `main` com **aprovação manual** via **GitHub Environments** (required reviewers) antes de aplicar.

## Versionamento de releases

- **Conventional Commits** + **tags SemVer**, com changelog automatizado (ex.: release-please).

## Aprovação de PR

- Branch protection na `main` exigindo **CI verde + 1 review** (CODEOWNERS).

## Decisões em aberto

> Nenhuma no momento.
