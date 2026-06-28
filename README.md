# Arquitetura de Referência

> Fonte da verdade das preferências de engenharia de software do Lucas.
> Repositório central e **standalone**: qualquer projeto, ferramenta de LLM ou pipeline de agente deve **apontar para ela** antes de construir, revisar ou propor software.
>
> **Versão atual: `1.0.0`** — a fonte canônica é o marcador `<!-- arquitetura_version: X.Y.Z -->` no topo do `CONSTITUTION.md`.
>
> **Comece identificando o modo da tarefa:** para **usar** a arquitetura (construir/revisar software com ela), vá ao [`MODO-DE-USO.md`](MODO-DE-USO.md); para **atualizar** a arquitetura (mudar/adicionar capítulos ou regras), vá ao [`MODO-DE-ATUALIZACAO.md`](MODO-DE-ATUALIZACAO.md). Detalhe na seção 2.

---

## 1. O que é

Esta pasta reúne, de forma estruturada, **as boas práticas, stacks, padrões e convenções** que o Lucas adota para construir software. Ela existe para que ferramentas de IA produzam código e decisões alinhadas às preferências dele, sem precisar perguntar tudo a cada interação.

É um **repositório standalone** que serve como fonte única: em vez de copiar regras para cada projeto, os projetos referenciam este repo.

Não é documentação de um projeto específico nem dependência de nenhuma ferramenta em particular: é a **camada de preferências transversal** que se aplica a todos os projetos, salvo quando um projeto declarar explicitamente o contrário. Funciona por si só — qualquer consumidor (humano, agente de IA ou pipeline) a usa lendo estes arquivos.

## 2. Como usar

Este `README.md` é o **índice e ponto de partida**. **Primeiro, identifique o modo da tarefa:**

- **Vai construir, revisar ou propor software seguindo estas preferências?** → **modo de uso**: leia o **`MODO-DE-USO.md`**. A arquitetura é **somente leitura**; você a aplica no projeto alvo, nunca edita os arquivos daqui.
- **Vai mudar a própria arquitetura** (editar/adicionar/remover capítulo, mudar uma regra, versionar)? → **modo de atualização**: leia o **`MODO-DE-ATUALIZACAO.md`**.

Atalhos por arquivo:

- **Projeto novo** → copie **`templates/CLAUDE.md`** para a raiz e preencha a seção "Específico deste projeto".
- **Régua verificável das regras** (avaliar PASS/FAIL) → **`CONSTITUTION.md`**.

> A precedência, a conduta e os não-negociáveis vivem no `MODO-DE-USO.md`, e a régua formal no `CONSTITUTION.md`. Não são repetidos aqui, para não divergirem.

## 3. Como está organizada

O repositório tem dois tipos de arquivo: **arquivos de suporte** (que explicam como usar, atualizar e versionar a arquitetura) e **temas da arquitetura** (`NN-*.md`, que descrevem as preferências em si).

### 3.1 Arquivos de suporte

| Arquivo | Papel |
|---|---|
| `README.md` | Índice canônico (este arquivo): o que é, como está organizado e para onde ir. |
| `MODO-DE-USO.md` | **Guia operacional para LLMs/agentes**: como navegar, precedência, conduta, fluxo de spec, autonomia, não-negociáveis e definição de pronto. O "como usar" consolidado. A arquitetura é somente leitura neste modo. |
| `MODO-DE-ATUALIZACAO.md` | **Guia para evoluir a arquitetura**: como uma mudança entra (capítulo + constituição), versionamento, manutenção e checklist. Usado **só** ao alterar/adicionar capítulos. |
| `CONSTITUTION.md` | **Régua canônica e verificável** da arquitetura. Carrega a versão (semver) no topo e condensa as regras em imperativos PASS/FAIL. É contra ela que specs e implementações são avaliadas. |
| `VERSIONAMENTO.md` | Política de versionamento (semver): quando incrementar MAJOR/MINOR/PATCH, como fazer um bump e por que versionar a régua. |
| `templates/CLAUDE.md` | **Ponto de entrada por projeto.** Template para copiar na raiz de um repositório: o Claude Code o lê automaticamente e, a partir dele, carrega as regras globais daqui. Tem uma seção "Específico deste projeto" a preencher. |

### 3.2 Temas da arquitetura

| Arquivo | Macro tema | Cobre |
|---|---|---|
| `01-arquitetura-do-projeto.md` | Arquitetura do código | Clean Architecture + Use Cases, DDD, tratamento de erros, Resilience4j |
| `02-stacks-tecnologicas.md` | Stacks tecnológicas | Java 21 + Maven, Python 3.13 (Lambdas), Spring Boot (REST) |
| `03-qualidade-e-testes.md` | Qualidade e testes | Cobertura mínima 95% por módulo, JUnit/JaCoCo, pytest, Testcontainers |
| `04-dados-e-persistencia.md` | Dados e persistência | DynamoDB on-demand, tabelas via Terraform, LocalStack |
| `05-observabilidade.md` | Observabilidade | Logs JSON estruturados (id, mensagem, horário, nível, correlationId) |
| `06-ci-cd-e-deploy.md` | CI/CD e deploy | GitHub Actions, feature branches → main, PR automático, ECR |
| `07-infraestrutura-e-ambientes.md` | Infraestrutura | AWS, Terraform, Docker, ambiente único, execução local |
| `08-governanca-e-documentacao.md` | Governança e documentação | README na raiz, ADR, Conventional Commits, OpenAPI, idioma pt-BR |
| `09-seguranca-e-segredos.md` | Segurança e segredos | Segredos fora do repo, Secrets Manager/SSM, OAuth2/JWT, TLS |
| `10-privacidade-e-lgpd.md` | Privacidade e LGPD | PII, minimização, não-logar dado pessoal, criptografia |
| `11-apis-e-contratos.md` | APIs e contratos | REST, versionamento, RFC 7807, OpenAPI |
| `12-configuracao.md` | Configuração | 12-factor, Spring Profiles, config por ambiente |
| `13-colaboracao-com-ia.md` | Colaboração com IA | Spec antes de codar, autonomia, checkpoints, definição de pronto |

> Estas tabelas são o índice canônico — mantê-las atualizadas ao adicionar, remover ou fundir arquivos.

## 4. Manutenção

Para **evoluir a arquitetura** (editar/adicionar capítulos, mudar regras, versionar), siga o **`MODO-DE-ATUALIZACAO.md`** — ele reúne as convenções de manutenção, a coerência capítulo↔constituição e o versionamento (`VERSIONAMENTO.md`).

## 5. Status

- **Versão:** `1.0.0` (ver `CONSTITUTION.md`).
- **Conteúdo:** 13 temas consolidados + arquivos de suporte (`MODO-DE-USO.md`, `MODO-DE-ATUALIZACAO.md`, `CONSTITUTION.md`, `VERSIONAMENTO.md`) e template de `CLAUDE.md`.
- **Maturidade:** pronto para ser usado como repositório remoto e referenciado pelos projetos.

---
