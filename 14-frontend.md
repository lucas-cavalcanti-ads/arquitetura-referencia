# 14 — Frontend

> **Propósito:** definir como construir interfaces web (SPAs) — stack, Design System, arquitetura da aplicação, acessibilidade e testes de front.
> **Como a IA deve usar:** ao criar ou evoluir um frontend, siga estas preferências antes de aplicar defaults. Justifique qualquer desvio. O que já é coberto por outros capítulos (testes, CI/CD, configuração, segredos, governança) é **referenciado**, não repetido.

---

## Stack e tooling

- **Linguagem:** TypeScript com `strict: true`. Sem `any` implícito — prefira `unknown` e tipos explícitos.
- **Configuração do compilador:** `target`/`lib` ES2022 + DOM; `module` ESNext; `moduleResolution: bundler`; ESM puro (`"type": "module"` no `package.json`), com **extensão `.js` explícita** nos imports relativos do código-fonte. Alias de import `@/* → src/*`.
- **Build/dev:** **Vite**. O build roda **type-check antes do bundle**: `build = tsc && vite build`. Falha de tipo quebra o build.
- **Gerenciador de pacotes:** **pnpm**. O lockfile (`pnpm-lock.yaml`) é commitado; o CI instala com `--frozen-lockfile`. Node 20.
- **Lint:** **ESLint** (flat config, `eslint.config.js`) + `typescript-eslint`. Script `lint` roda sobre `src/`.
- **Sem framework de UI** (React/Angular/Vue): a app é TypeScript sobre o DOM. Componentes não usam JSX.

## Design System (Material 3)

- **Design System:** **Material Design 3 (M3)**, via `@material/web`.
- **Cor sempre por token.** A paleta vem dos tokens de sistema do M3 (`--md-sys-color-primary`, `--md-sys-color-surface`, `--md-sys-color-on-*`, `--md-sys-color-outline`, …). **Nenhuma cor hardcoded** fora da camada de tokens.
- **Camada semântica do projeto.** Sobre os tokens M3, defina tokens do app com prefixo próprio (ex.: `--ep-spacing-*` na escala 4/8/16/24/32, `--ep-*` de layout). Espaçamento e dimensões saem desses tokens, não de números soltos.
- **Componentes.** Prefira os web components do `@material/web` (`<md-*>`) quando houver equivalente direto (campos de formulário, botão, dialog). Para layout e composições sem equivalente, use **CSS próprio tematizado** (classes com prefixo do app, ex.: `.ep-*`) — apoiado nos tokens M3. Não reinventar componente que o Material Web já entrega.
- **Tipografia e ícones:** Roboto + Material Icons.
- **CSS:** folha de estilo própria com os tokens. Sem Tailwind nem CSS-in-JS.
- **Responsividade:** mobile-first pragmático, com breakpoints em `768px` e `480px` (drawer colapsa, grids reflowam).

## Arquitetura da aplicação

Eco do Clean Architecture do backend (ver `01-arquitetura-do-projeto.md`), na escala de um front: camadas explícitas e dependências apontando para dentro.

- **Camadas/diretórios:** `api/` (cliente HTTP tipado + recursos por domínio), `components/` (renderizadores reutilizáveis), `pages/` (uma tela por rota), `router.ts` (roteamento), `types.ts`, `utils.ts`, `styles/`.
- **Acesso ao backend só pela camada `api/`.** Páginas e componentes **não** chamam `fetch` direto. A camada expõe helpers tipados (`apiGet<T>`, `apiPost<T>`, `apiPut<T>`, `apiPostForm`, `apiGetBlob`) sobre um único wrapper.
- **Erros normalizados.** O wrapper traduz falha de rede e respostas 4xx/5xx num tipo de erro próprio (ex.: `ApiError { status, message }`), extraindo a mensagem do backend quando houver. Nada de erro cru vazando para a UI.
- **Componentes** são funções `render*()` com export nomeado, que montam o DOM da sua área. Estado e efeitos colaterais ficam contidos e explícitos.
- **Roteamento** próprio, hash-based (`#/`, `#/recurso/:id`), com registro de rotas, navegação programática e fallback para a raiz.

## Acessibilidade (a11y)

- Todo elemento interativo tem **rótulo acessível** (`aria-label`/texto) e **papel** correto (`role`).
- Regiões dinâmicas usam `aria-live` quando o conteúdo muda sem recarregar; ícones decorativos são `aria-hidden`.
- A interface é **navegável por teclado** (`tabindex`, foco visível, ordem lógica).

## Configuração por ambiente

Segue 12-factor (ver `12-configuracao.md`) e a regra de segredos (ver `09-seguranca-e-segredos.md`).

- Config vem do ambiente via `import.meta.env` (ex.: `VITE_API_URL`), com default sensato para dev (proxy do Vite para o backend local, sem CORS).
- **Nenhum segredo no bundle** — o que vai para o front é público. Há `.env.example` documentando as variáveis.

## Testes

Segue a estratégia e a cobertura de `03-qualidade-e-testes.md`; aqui ficam só as ferramentas e onde cada nível incide.

- **Unitário:** **Vitest** — cobre os módulos de lógica (`api/`, `utils`, `router`, transformações). A régua de cobertura do `03` (≥95% por módulo) recai sobre essa camada.
- **E2E:** **Playwright** — cobre fluxos de tela e a camada de render/DOM (`components/`, `pages`), que não é alvo de cobertura unitária.
- Scripts canônicos: `test` (vitest run), `test:watch`, `test:e2e`.

## CI/CD

Segue `06-ci-cd-e-deploy.md`; particularidades do front:

- **GitHub Actions** com jobs `lint`, `test` e `build`, sendo `build` dependente de `lint` + `test`. Todos verdes são condição de merge.
- pnpm + Node 20 com `--frozen-lockfile`; o artefato de build (`dist/`) é publicado pelo job de build.

## Idioma

- Texto de UI em **Português (Brasil)**, inline no código (ver `08-governanca-e-documentacao.md`). Sem biblioteca de i18n enquanto a aplicação for monolíngue.

## Decisões em aberto

> Nenhuma no momento.
