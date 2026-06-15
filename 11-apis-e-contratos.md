# 11 — APIs e Contratos

> **Propósito:** padrão mínimo para APIs REST.
> **Como a IA deve usar:** ao gerar uma API REST (Spring Boot), seguir estas convenções.
> **Escopo:** intencionalmente enxuto.

---

## Padrão

- **REST com Spring Boot** (ver `02-stacks-tecnologicas.md`).
- **Versionamento por path:** `/v1/...`.
- **Recursos** nomeados como substantivos no plural (`/v1/pedidos`); usar os verbos HTTP corretos (GET, POST, PUT, PATCH, DELETE) e status codes adequados.
- **Erros padronizados** no formato **RFC 7807 (Problem Details)** — corpo de erro consistente com `type`, `title`, `status`, `detail`.
- **Paginação** em endpoints que retornam listas.
- **Documentação OpenAPI/Swagger** gerada automaticamente (ver `08-governanca-e-documentacao.md`).

## Decisões em aberto

> _A preencher se necessário: estratégia de paginação (offset vs. cursor), convenção de filtros/ordenação, política de evolução/compatibilidade de contrato._
