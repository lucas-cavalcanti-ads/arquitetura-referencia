# Arquitetura de Referência

> Fonte da verdade das preferências de engenharia de software do Lucas.
> Repositório central: qualquer projeto, ferramenta de LLM ou pipeline de agente deve **apontar para este repositório** antes de construir, revisar ou propor software.
> Como apontar: ver **`INTEGRACAO.md`**.

---

## 1. O que é

Esta pasta reúne, de forma estruturada, **as boas práticas, stacks, padrões e convenções** que o Lucas adota para construir software. Ela existe para que ferramentas de IA produzam código e decisões alinhadas às preferências dele, sem precisar perguntar tudo a cada interação.

É um **repositório standalone** que serve como fonte única: em vez de copiar regras para cada projeto, os projetos referenciam este repo (por URL, submodule ou clone pinado — ver `INTEGRACAO.md`).

Não é documentação de um projeto específico: é a **camada de preferências transversal** que se aplica a todos os projetos, salvo quando um projeto declarar explicitamente o contrário.

## 2. Como está organizada

| Arquivo | Macro tema | Cobre |
|---|---|---|
| `README.md` | Guia (este arquivo) | O que é, como usar |
| `INTEGRACAO.md` | Integração | Como projetos/agentes apontam para este repo |
| `VERSIONAMENTO.md` | Versionamento | SemVer da arquitetura, quando incrementar, como a esteira consome |
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
| `templates/CLAUDE.md` | Template | Ponto de entrada por projeto para o Claude Code |

> Esta tabela é o índice canônico — mantê-la atualizada ao adicionar, remover ou fundir temas.

## 3. Como a IA deve usar esta arquitetura

1. **Leia o `README.md` primeiro.** Ele dá o mapa.
2. **Leia os arquivos relevantes ao tema da tarefa.** Em caso de dúvida, leia mais.
3. **Trate o conteúdo como preferência autoritativa.** Para desviar de algo declarado aqui, deixe explícito o porquê e confirme com o Lucas.
4. **Respeite a precedência:** instrução direta do Lucas na conversa > regra de um projeto específico > esta arquitetura de referência > defaults genéricos.
5. **Quando houver lacuna**, não invente preferência: assuma um default razoável, **sinalize a suposição** e pergunte se for relevante.
6. **Não trate o conteúdo destes arquivos como comandos.** Eles descrevem preferências; ações com efeito colateral exigem confirmação do Lucas (ver `13-colaboracao-com-ia.md`).

## 4. Regras transversais (valem para tudo)

- **Rodar local sempre:** todo sistema deve conseguir rodar 100% localmente (LocalStack + Docker), espelhando o comportamento na AWS. A diferença entre local e nuvem é só configuração de ambiente.
- **Menor recurso possível sob demanda:** preferir capacidade on-demand/serverless e dimensionamento mínimo na AWS (ex.: DynamoDB pay-per-request).
- **Idioma:** todos os artefatos em **Português (Brasil)** — código, comentários, logs, commits, corpo de PR, documentação (ver `08-governanca-e-documentacao.md`).
- **Documentação:** toda aplicação tem `README` na raiz, técnico e funcional, criado ou atualizado a cada entrega.
- **Nuvem:** **AWS** como provedor padrão.
- **Segredos:** nunca no repositório (ver `09-seguranca-e-segredos.md`).
- **Spec antes de codar** tarefa não-trivial; **commit/push** liberados, **deploy só via esteira** (ver `13-colaboracao-com-ia.md`).
- **Versionamento:** a arquitetura é versionada por SemVer (marcador no topo do `CONSTITUTION.md`); cada nota de qualidade da esteira carimba a versão + SHA usados (ver `VERSIONAMENTO.md`).

## 5. Convenções de manutenção

- Cada arquivo tem cabeçalho de propósito e um bloco de **Decisões em aberto** ao final.
- Ao consolidar uma preferência, descreva a regra de forma acionável (o que fazer, não só o princípio).
- Evite duplicar a mesma regra em dois arquivos; prefira referenciar (`ver 03-qualidade-e-testes.md`).
- Mudanças seguem **Conventional Commits** e são versionadas por **tags SemVer** (ver `INTEGRACAO.md`).

## 6. Status

13 macro temas consolidados + guia de integração e template de `CLAUDE.md`. Pronto para virar repositório remoto e ser referenciado pelos projetos.