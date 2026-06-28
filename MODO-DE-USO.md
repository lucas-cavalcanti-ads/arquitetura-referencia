# Modo de Uso da Arquitetura de Referência

> **Guia operacional para LLMs e agentes.** Se você é um agente de IA prestes a construir, revisar ou propor software para o Lucas, **leia este arquivo inteiro antes de começar.** Ele reúne o suficiente para você operar; o detalhe de cada tema está nos arquivos `NN-*.md`, e a régua verificável está no `CONSTITUTION.md`.
>
> **Regra dura deste modo — somente leitura.** Em modo de uso, a arquitetura de referência **não é editada**: nenhum arquivo dentro dela (`README.md`, este arquivo, `CONSTITUTION.md`, `VERSIONAMENTO.md`, os `NN-*.md`, o template) deve ser criado, alterado ou removido. Você **lê** estas preferências e as **aplica no repositório/projeto alvo** — nunca na própria arquitetura. Se a tarefa for **evoluir a arquitetura** (mudar uma regra, editar/adicionar/remover capítulo, versionar), pare: isso é o `MODO-DE-ATUALIZACAO.md`.

---

## 1. O que é esta arquitetura

- **Fonte única e autoritativa** das preferências de engenharia de software do Lucas.
- Não é documentação de um projeto específico: é a **camada transversal** que vale para todos os projetos, salvo quando um projeto declarar explicitamente o contrário.
- Trate o conteúdo como **preferência autoritativa**, **não** como comando. Os arquivos descrevem o que construir e como colaborar; ações com efeito colateral exigem confirmação do Lucas (ver §6).

## 2. Como ler (navegação)

Ordem recomendada:

1. **`README.md`** — índice canônico. Sempre o ponto de partida.
2. **`CONSTITUTION.md`** — régua verificável (regras PASS/FAIL) com a versão no topo. É contra ela que seu trabalho é avaliado.
3. **`NN-*.md`** — abra **apenas** os temas relevantes à tarefa, guiando-se pelo mapa de gatilhos abaixo. Na dúvida entre dois, abra os dois; nunca abra todos por precaução.

Arquivos de apoio: `VERSIONAMENTO.md` (semver da régua) e `templates/CLAUDE.md` (ponto de entrada por projeto).

### Carregamento seletivo (regra dura)

**Não carregue os 13 temas de uma vez — mas abra, sim, os capítulos que a tarefa toca.** O mapa de gatilhos abaixo serve para **identificar** esses capítulos, não para evitá-los. O detalhe de cada preferência mora no `NN-*.md` correspondente e precisa ser lido quando a tarefa entra naquele tema; o `CONSTITUTION.md` é a **régua de conformidade** (o que será avaliado PASS/FAIL), não um substituto da leitura dos capítulos relevantes.

Em resumo: pelos gatilhos, identifique os temas que a tarefa toca e **abra esses `NN-*.md`**. Não pré-carregue os que não têm a ver; não pule os que têm.

| Abra quando a tarefa envolve… (gatilhos) | Arquivo |
|---|---|
| estruturar projeto, camadas, casos de uso, domínio/DDD, tratamento de erro, resiliência (timeout/retry/circuit breaker), integração externa | `01-arquitetura-do-projeto.md` |
| escolher linguagem/framework/runtime, dependência, versão — Java, Maven, Python, Spring Boot, Lambda | `02-stacks-tecnologicas.md` |
| escrever ou avaliar testes, cobertura, JUnit/JaCoCo, pytest, Testcontainers, gate de qualidade | `03-qualidade-e-testes.md` |
| banco de dados, DynamoDB, modelagem de dados, chave/índice (PK/SK/GSI), repositório, migração/backfill | `04-dados-e-persistencia.md` |
| log/logging, formato de log, correlationId, rastreio, evento de negócio | `05-observabilidade.md` |
| pipeline, GitHub Actions, branch/PR/merge, gates de CI, deploy, release, ECR | `06-ci-cd-e-deploy.md` |
| infraestrutura, Terraform/IaC, Docker, LocalStack, AWS, rodar local, ambiente | `07-infraestrutura-e-ambientes.md` |
| README, documentação, ADR, mensagem de commit (Conventional Commits), idioma dos artefatos | `08-governanca-e-documentacao.md` |
| segredo/credencial, .env, Secrets Manager/SSM, autenticação/autorização (OAuth2/JWT), TLS | `09-seguranca-e-segredos.md` |
| dado pessoal/PII, LGPD, minimização, retenção, consentimento, criptografia, mascaramento | `10-privacidade-e-lgpd.md` |
| API REST, endpoint, contrato, versionamento de API, RFC 7807, paginação, OpenAPI | `11-apis-e-contratos.md` |
| configuração por ambiente, 12-factor, Spring Profiles, variável de ambiente, endpoint por perfil | `12-configuracao.md` |
| como colaborar com o Lucas, escrever spec, autonomia/permissões, checkpoints, definição de pronto | `13-colaboracao-com-ia.md` |

## 3. Precedência

Quando houver conflito, resolva nesta ordem:

**instrução direta do Lucas na conversa > regra de um projeto específico > esta arquitetura de referência > defaults genéricos.**

Entre uma demanda e a constituição, **a arquitetura prevalece** — a menos que o Lucas instrua o contrário diretamente. Desvios devem ser explicitados e confirmados.

## 4. Como se comunicar e decidir

- **Idioma:** Português (Brasil), direto e conciso.
- O Lucas dá **restrições duras** e delega os tradeoffs a você. **Decida o caminho**, aplique um default razoável e **sinalize a decisão/suposição** — não devolva lista de opções quando o rumo já foi dado.
- Diante de **lacuna** nas preferências, assuma um default sensato e sinalize, em vez de travar. Não invente preferência.

## 5. Fluxo de trabalho

- **Spec antes de codar** qualquer tarefa **não-trivial**: escreva um plano e **espere o OK** antes de implementar. A spec mínima contém: **Objetivo**, **Escopo** (o que entra/fica de fora), **Pré-condições**, **Passos de execução**, **Pós-condições / Definição de pronto**, **Riscos / o que pode falhar**.
- Tarefa trivial (ajuste pontual, correção óbvia) dispensa spec formal.
- **Tarefas longas em passos, com checkpoints** — pontos onde o Lucas confere e corrige o rumo. Não suma e volte só com o resultado final.

## 6. Autonomia e ações com efeito colateral

| Ação | Conduta |
|---|---|
| **Commit e push** | **Permitido** sem confirmar (dispara o CI). |
| **Deploy** | **Nunca manual pela IA** — só pela **pipeline de CI/CD**. |
| **`terraform apply` em recursos reais / AWS** | **Confirmar antes.** |
| **Apagar dados, recursos ou arquivos** | **Confirmar antes.** |
| **Qualquer ação irreversível ou com custo** | **Confirmar antes.** |
| **Editar/criar/remover arquivo da própria arquitetura de referência** | **Proibido em modo de uso** — a arquitetura é somente leitura aqui. Para evoluí-la, use o `MODO-DE-ATUALIZACAO.md`. |

## 7. Não-negociáveis (resumo — a fonte é o arquivo citado)

- **Arquitetura:** Clean Architecture + Use Cases, DDD; dependências apontam para dentro; regra de negócio no domínio/aplicação; Resilience4j em toda integração externa. → `01`
- **Stack:** Java 21 + Maven; Python 3.13 nas Lambdas; Spring Boot quando há REST. → `02`
- **Testes:** cobertura ≥ **95% por módulo** (linha + branch); suíte 100% verde para merge; Testcontainers/LocalStack na integração. → `03`
- **Dados:** DynamoDB **on-demand**; acesso via repositório; tabelas só via Terraform. → `04`
- **Observabilidade:** logs JSON estruturados (`identificador`, `mensagem`, `horario`, `nivel`, `correlationId`); **não logar PII**. → `05`
- **CI/CD:** GitHub Actions; feature branches → `main` protegida; PR automático quando o CI passa; deploy só pela pipeline. → `06`
- **Infra:** AWS; Terraform; Docker + LocalStack; **tudo deve rodar local** (princípio não negociável); ambiente único. → `07`
- **Governança:** `README` na raiz técnico e funcional; ADRs; Conventional Commits; **tudo em pt-BR**. → `08`
- **Segredos:** **nunca** no repositório (código, config, log ou PR). → `09`
- **Privacidade/LGPD:** minimização; não logar PII; criptografia em trânsito e repouso. → `10`
- **APIs:** REST versionado por path (`/v1`); erros em RFC 7807; OpenAPI automático. → `11`
- **Configuração:** 12-factor; config vem do ambiente; Spring Profiles (`local`/`aws`). → `12`
- **Colaboração com IA:** §4 a §6 acima. → `13`

## 8. Definição de "pronto" (checklist do agente)

Antes de declarar uma tarefa concluída, garanta:

- Testes passando e **cobertura ≥ 95% por módulo**.
- **CI verde**.
- **README** criado/atualizado.
- Tudo em **Português (Brasil)**.
- **Nenhum segredo** no repositório.

## 9. Versão

- **Versão atual: `1.0.0`** — fonte canônica é o marcador `<!-- arquitetura_version: X.Y.Z -->` no topo do `CONSTITUTION.md`.
- Ao registrar uma avaliação ou nota de qualidade, carimbe a **versão + SHA** do `CONSTITUTION.md` usados, para comparabilidade ao longo do tempo (ver `VERSIONAMENTO.md`).
