# Versionamento da Arquitetura de Referência

A arquitetura de referência é **versionada** (semver). A versão vive no marcador da primeira linha do
`CONSTITUTION.md`:

```
<!-- arquitetura_version: X.Y.Z -->
```

Esse arquivo (`CONSTITUTION.md`) é a expressão canônica e verificável da arquitetura — a régua contra
a qual specs e implementações são avaliadas. Versionar a arquitetura = versionar essa régua.

## Por que versionar

A esteira de refinamento/desenvolvimento grava, junto de **cada nota de qualidade**, a versão da
arquitetura usada (`arquitetura_version`) **e** o SHA do commit do `CONSTITUTION.md`. Isso permite,
ao longo do tempo, distinguir duas coisas que de outra forma se confundiriam:

- **"A qualidade caiu"** — as notas baixaram contra a mesma régua.
- **"A régua mudou"** — a arquitetura evoluiu (nova versão), então notas antigas e novas não são
  diretamente comparáveis.

A versão semântica responde "qual conjunto de regras"; o SHA responde "exatamente quais bytes".

## Quando incrementar

| Incremento | Quando | Efeito nas notas |
|---|---|---|
| **MAJOR** (X) | Uma regra existente muda de forma incompatível — código antes conforme passa a violar (ex: trocar o padrão de camadas, mudar o banco padrão). | Quebra de série: compare notas só dentro da mesma major. |
| **MINOR** (Y) | Regra nova **aditiva** — aperta a régua sem invalidar o que já era conforme (ex: passar a exigir teste de contrato em todo endpoint). | Notas podem cair em itens novos; sinalize o bump na análise de tendência. |
| **PATCH** (Z) | Esclarecimento ou correção de redação, sem mudar a exigência. | Comparável; sem quebra de série. |

## Como fazer um bump

1. Edite as regras no `CONSTITUTION.md`.
2. Atualize o número em **dois lugares**: o marcador `<!-- arquitetura_version: X.Y.Z -->` no topo e
   o campo **Versão** em "Metadados".
3. Adicione uma linha no **Histórico de versões** do `CONSTITUTION.md`.
4. Commite (de preferência via PR). O commit fixa o SHA que a esteira vai carimbar.
5. O próximo run da esteira lê a nova versão automaticamente (do `local_path` ou via clone) e passa a
   carimbá-la nas notas.

## Como a esteira consome

O script `fetch-constitution.sh` da esteira lê o `CONSTITUTION.md` deste repo, extrai o marcador de
versão e o SHA do commit, e materializa a constituição para o run. Nada é inferido de código: é
leitura determinística do arquivo versionado. Detalhes em `esteira-refin-desenv-v1/README.md`.
