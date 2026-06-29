<!-- arquitetura_version: 1.1.0 -->
<!-- Régua canônica de conformidade da arquitetura de referência.
     A esteira grava a versão semântica acima e o SHA do commit junto de cada nota. -->

# Constituição — Arquitetura de Referência

Régua canônica de conformidade da arquitetura de referência. Toda especificação e implementação
produzidas pela esteira são avaliadas contra estas regras. As regras são prescritivas e verificáveis;
em conflito entre uma demanda e esta constituição, **a arquitetura de referência prevalece**.

## Metadados

- **Versão da arquitetura de referência:** 1.1.0
- **Última atualização:** 2026-06-28
- **Versionamento:** toda mudança de regra incrementa esta versão (semver) e o marcador
  `<!-- arquitetura_version: X.Y.Z -->` no topo. A esteira grava esta versão **e** o SHA do commit
  junto de cada nota, para comparabilidade ao longo do tempo. Política detalhada em
  `VERSIONAMENTO.md`.

## Princípios de redação das regras

- **Prescritivo e verificável**: imperativos que um revisor julga PASS/FAIL.
- **Poucas regras fortes** valem mais que muitas regras vagas.

---

## 1. Arquitetura do projeto

- Clean Architecture com DDD. As dependências apontam sempre **para dentro**: o domínio não conhece
  infraestrutura nem framework.
- Camadas explícitas e separadas: domínio (entidades e regras), aplicação (casos de uso),
  interface/adapters, infraestrutura.
- Regra de negócio vive no domínio/aplicação — **nunca** em controllers ou em código de framework.
- Convenções de pacotes/módulos e nomenclatura das camadas seguem `01-arquitetura-do-projeto.md`.

## 2. Stacks tecnológicas

- Backend em **Java 21**; build com **Maven**.
- Framework de aplicação: **Spring Boot**.
- Funções serverless (AWS Lambda) em **Python 3.13**.
- Toda integração externa usa **Resilience4j** (timeout, retry e circuit breaker explícitos).
- Versões mínimas de bibliotecas e módulos padrão do Spring seguem `02-stacks-tecnologicas.md`.

## 3. Qualidade e testes

- Todo código novo é coberto por testes automatizados.
- Pirâmide de testes: unitários na base, integração no meio, e2e no topo.
- A suíte passa 100% (zero falhas) como condição de merge.
- A cobertura mínima exigida e as ferramentas padrão seguem `03-qualidade-e-testes.md`.

## 4. Dados e persistência

- Banco: **DynamoDB** em modo **on-demand**.
- Acesso a dados **sempre** via camada de repositório; sem uso direto do SDK do DynamoDB fora dela.
- Modelagem orientada aos padrões de acesso.
- Estratégia de tabela, convenções de chave (PK/SK), índices e migração seguem
  `04-dados-e-persistencia.md`.

## 5. Observabilidade

- Logs estruturados, em formato consistente, nos pontos de entrada, saída e falha.
- Toda falha de integração externa é logada com contexto suficiente para diagnóstico.
- Métricas obrigatórias, tracing distribuído e correlação de IDs seguem `05-observabilidade.md`.

## 6. CI/CD e deploy

- Pipeline em **GitHub Actions**.
- Merge exige build verde + testes passando + checks de qualidade.
- Etapas obrigatórias do pipeline, gates e estratégia de deploy seguem `06-ci-cd-e-deploy.md`.

## 7. Infraestrutura e ambientes

- **Tudo deve rodar localmente — princípio NÃO NEGOCIÁVEL.** Nenhuma funcionalidade depende de
  recursos que só existem na nuvem para ser desenvolvida e testada.
- IaC com **Terraform**.
- Ambiente local com **Docker** e **LocalStack** para emular serviços AWS.
- Serviços emulados e procedimento de subida local seguem `07-infraestrutura-e-ambientes.md`.

## 8. Governança e documentação

- Decisões arquiteturais relevantes viram **ADR**.
- Toda entrega satisfaz a **Definition of Done**.
- Os itens do DoD e a documentação obrigatória por entrega seguem `08-governanca-e-documentacao.md`.

## 9. Segurança e segredos

- Segredos **nunca** em código ou repositório; sempre via cofre/variáveis de ambiente.
- O mecanismo de gestão de segredos e as regras de autenticação/autorização seguem
  `09-seguranca-e-segredos.md`.

## 10. Privacidade e LGPD

- Dados pessoais tratados sob **minimização** (coletar apenas o necessário).
- Regras de retenção, anonimização e consentimento seguem `10-privacidade-e-lgpd.md`.

## 11. APIs e contratos

- Todo endpoint expõe contrato **OpenAPI**.
- Mudança de contrato público exige **versionamento**.
- Cada endpoint tem teste de contrato/integração.
- O padrão de versionamento e as convenções REST seguem `11-apis-e-contratos.md`.

## 12. Configuração

- Configuração **externalizada** do código (sem valores de ambiente hardcoded).
- A hierarquia de configuração por ambiente e as fontes seguem `12-configuracao.md`.

## 13. Colaboração com IA

- Agentes de IA seguem a **tabela de autonomia**: o que podem fazer sozinhos vs. o que exige
  aprovação humana.
- A IA respeita todas as regras desta constituição; em conflito, a arquitetura prevalece.
- A tabela de autonomia e as regras de colaboração seguem `13-colaboracao-com-ia.md`.

## 14. Frontend

- Frontend em **TypeScript** com `strict: true`; o build roda **type-check antes do bundle** (`tsc && vite build`).
- Build/dev com **Vite**; pacotes com **pnpm** (lockfile commitado; `--frozen-lockfile` no CI).
- Design System **Material 3**: cor sempre via tokens (`--md-sys-color-*` + camada semântica do app); **nenhuma cor hardcoded** fora da camada de tokens.
- Camadas separadas (`api`, `components`, `pages`, `router`); acesso ao backend **só pela camada `api/`** tipada — sem `fetch` solto em páginas/componentes.
- Acessibilidade: todo interativo com **rótulo acessível** e **navegável por teclado**.
- Testes de front com **Vitest** (unitário) e **Playwright** (e2e); cobertura segue a régua do §3.
- Detalhe e convenções em `14-frontend.md`.

---

## Exceções concedidas

Exceções a estas regras são **por-demanda**, registradas como ADR em
`refinamentos-gen-ai/<slug>/decisoes/`. Uma exceção **não** altera esta constituição; mudança
durável é feita via PR a este arquivo (com bump de versão).

## Histórico de versões

| Versão | Data | Mudança |
|---|---|---|
| 1.0.0 | 2026-06-18 | Versão inicial em uso. |
| 1.1.0 | 2026-06-28 | Adiciona o capítulo 14 (Frontend): TypeScript + Vite + pnpm, Design System Material 3, arquitetura de SPA, a11y e testes de front. |
