# 05 — Observabilidade

> **Propósito:** definir como a aplicação registra sua história em logs.
> **Como a IA deve usar:** todo log gerado deve seguir o formato estruturado abaixo. Logs são a narrativa funcional da aplicação, não ruído de debug.

---

## Princípio

- Os logs devem ser **funcionais** e contar **toda a história da aplicação**: ao ler os logs, deve ser possível reconstruir o que aconteceu em uma execução, do início ao fim.
- Log é parte do comportamento da aplicação, não um adendo. Eventos de negócio relevantes e erros devem deixar rastro.

## Biblioteca de logging

- **Java:** SLF4J + Logback com `logstash-logback-encoder` (saída em **JSON**).
- Logs vão para **stdout** → coletados pelo CloudWatch na AWS.

## Formato obrigatório do log

Cada log é **exposto como objeto** (log estruturado) e contém, no mínimo:

| Campo | Descrição |
|---|---|
| `identificador` | Identificador único que localiza o log dentro do código. |
| `mensagem` | Mensagem descritiva do evento. |
| `horario` | Timestamp do evento (ver formato abaixo). |
| `nivel` | Nível do log (INFO, WARN, ERROR, etc.). |
| `correlationId` | Identificador de correlação por requisição/execução, para rastreio ponta a ponta. |

Exemplo conceitual:

```json
{
  "identificador": "PEDIDO_CRIADO_001",
  "mensagem": "Pedido criado com sucesso",
  "horario": "2026-06-14T14:32:07.482-03:00",
  "nivel": "INFO",
  "correlationId": "a1b2c3d4-..."
}
```

## Convenção do `identificador`

- Padrão: **`DOMINIO_EVENTO_NNN`** (ex.: `PEDIDO_CRIADO_001`).
- Centralizar os identificadores em um **catálogo único** (enum/`record` Java implementando uma interface comum, ex.: `EventoLog`). Isso garante unicidade e permite localizar, a partir do log, exatamente qual ponto do código o emitiu.

## Formato do timestamp

- **Apresentação mínima legível:** `aaaa-mm-dd h:mm:ss`.
- **Gravação interna:** **ISO-8601 com offset e milissegundos** — `2026-06-14T14:32:07.482-03:00` — para não perder timezone nem precisão em investigação de incidente.

## Tracing distribuído

- Não adotar por ora. O `correlationId` cobre a necessidade de rastreio atual. Reavaliar se/quando houver múltiplos serviços.

## Cuidado com dados sensíveis

- Como o log "conta toda a história", atenção para **não vazar PII / dados sensíveis** em mensagens. Mascarar quando necessário.

## Decisões em aberto

> Nenhuma no momento.
