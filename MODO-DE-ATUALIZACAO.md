# Modo de Atualização da Arquitetura de Referência

> **Guia operacional para evoluir a própria arquitetura de referência.** Use este modo quando a tarefa é **mudar a arquitetura em si** — não construir software com ela. Se a tarefa é construir, revisar ou propor software seguindo as preferências, o modo é o outro: `MODO-DE-USO.md`.
>
> **Regra dura deste modo.** Aqui você **edita os arquivos da arquitetura de referência** — e **somente** eles. Não é hora de implementar features de um projeto alvo; as alterações ficam contidas neste repositório. (No modo de uso vale o oposto: a arquitetura é somente leitura.)

---

## 1. Quando este modo se aplica

- Editar, refinar ou corrigir um capítulo (`NN-*.md`).
- Adicionar, remover ou fundir um capítulo.
- Mudar uma regra ou ajustar a constituição (`CONSTITUTION.md`).
- Atualizar o índice (`README.md`) ou o mapa de gatilhos (`MODO-DE-USO.md`).

Se a tarefa não é nenhuma dessas, você está em **modo de uso** — volte ao `MODO-DE-USO.md`.

## 2. Como uma mudança entra

1. **Spec antes de mudança não-trivial.** Escreva o que vai mudar e por quê, e **espere o OK do Lucas** antes de aplicar. Valem as mesmas regras de colaboração do `MODO-DE-USO.md` (§4 a §6) e do `13-colaboracao-com-ia.md`. Ajuste pontual/óbvio dispensa spec formal.
2. **Detalhe no capítulo, régua na constituição.** O detalhe da preferência vive no `NN-*.md`. Se a mudança altera uma **exigência**, reflita o imperativo correspondente no `CONSTITUTION.md`, para que capítulo e régua fiquem coerentes.
3. **Versione.** Toda mudança de regra incrementa a versão (semver) no marcador `<!-- arquitetura_version: X.Y.Z -->` do `CONSTITUTION.md` e registra uma linha no histórico de versões dele. Quando incrementar MAJOR/MINOR/PATCH e como bumpar: `VERSIONAMENTO.md`.
4. **Mantenha o roteador em dia.** Se você adicionou, removeu ou fundiu um capítulo, atualize o índice no `README.md` (seção "Como está organizada") **e** o mapa de gatilhos no `MODO-DE-USO.md` (seção "Carregamento seletivo") — senão o carregamento seletivo fica cego para o novo tema.

## 3. Convenções de manutenção

- Cada capítulo tem cabeçalho de propósito e um bloco de **Decisões em aberto** ao final.
- Descreva a regra de forma **acionável** (o que fazer, não só o princípio).
- **Não duplique** a mesma regra em dois arquivos; prefira referenciar (`ver 03-qualidade-e-testes.md`).
- Commits em **Conventional Commits**; mudanças versionadas por **tags SemVer** (ver `VERSIONAMENTO.md`).
- Todos os artefatos em **Português (Brasil)**.

## 4. Definição de "pronto" de uma atualização

Antes de declarar a atualização concluída, garanta:

- Capítulo (`NN-*.md`) e `CONSTITUTION.md` **coerentes** entre si.
- Se mudou uma exigência: **versão bumpada** no `CONSTITUTION.md` + linha no histórico de versões.
- Se mexeu na lista de capítulos: **índice** (`README.md`) e **mapa de gatilhos** (`MODO-DE-USO.md`) atualizados.
- Convenções de manutenção respeitadas; tudo em **pt-BR**.
- Commit em **Conventional Commits**.
