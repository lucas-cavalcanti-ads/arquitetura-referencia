# Como referenciar esta Arquitetura de Referência

> Este repositório é a **fonte única** das preferências de engenharia. Qualquer projeto, ferramenta de LLM ou pipeline de agente deve **apontar para ele** em vez de copiar as regras.
> Substitua `<OWNER>` pelo dono do repositório (ex.: seu usuário/organização no GitHub) nos exemplos abaixo.

---

## Ponto de entrada

- **Índice canônico:** `README.md` (lista todos os macro temas).
- A partir dele, abrir os arquivos `NN-*.md` do(s) tema(s) relevante(s).
- URL do repositório: `https://github.com/<OWNER>/arquitetura-referencia`

## Formas de referenciar

### A) Por URL — agentes de LLM, geração de specs, celular, qualquer ferramenta

Use quando o agente consegue acessar a web. Aponte para o repositório (ou para os arquivos raw) e deixe o agente buscar.

- Repo: `https://github.com/<OWNER>/arquitetura-referencia`
- Raw de um arquivo: `https://raw.githubusercontent.com/<OWNER>/arquitetura-referencia/main/README.md`

**Bloco pronto para colar** em system prompt / instrução de agente (dev ou gerador de specs):

```
Antes de qualquer trabalho de software, leia a Arquitetura de Referência em
https://github.com/<OWNER>/arquitetura-referencia (comece pelo README.md e abra
os arquivos NN-*.md do tema da tarefa). Trate-a como preferência autoritativa.
Para tarefas não-triviais, produza primeiro uma spec conforme 13-colaboracao-com-ia.md
e aguarde aprovação. Todos os artefatos em Português (Brasil).
```

### B) Git submodule — projetos e pipelines determinísticos

Use quando o agente/CI precisa dos arquivos localmente, de forma reprodutível e versionada.

```bash
git submodule add https://github.com/<OWNER>/arquitetura-referencia .arquitetura-referencia
git commit -m "chore: adiciona arquitetura de referência como submodule"
# em outra máquina / no CI:
git submodule update --init --recursive
```

Os arquivos ficam em `.arquitetura-referencia/` dentro do projeto.

### C) Clone raso pinado por versão — CI/CD

Use em esteiras onde você quer fixar uma versão específica:

```bash
git clone --depth 1 --branch v1.0.0 \
  https://github.com/<OWNER>/arquitetura-referencia /tmp/arq-ref
```

## Versionamento

- O repositório usa **tags SemVer** (`v1.0.0`, `v1.1.0`, ...) com **Conventional Commits** (mesma convenção de `08-governanca-e-documentacao.md`).
- **Produção/CI:** pine uma tag (`v1.x.x`) para builds reprodutíveis.
- **Exploração/dev:** referenciar `main` é aceitável.

## Recomendação por uso

| Cenário | Forma |
|---|---|
| Conversa com LLM (Claude, outra ferramenta, celular) | **A) URL** |
| Claude Code em um projeto | **A) URL** via `CLAUDE.md` (ver `templates/CLAUDE.md`) |
| Pipeline de agente que gera specs | **A) URL** (ou C, se quiser pinar) |
| Projeto/CI que precisa dos arquivos offline e reprodutíveis | **B) submodule** ou **C) clone pinado** |
