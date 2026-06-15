# 01 — Arquitetura do Projeto

> **Propósito:** definir como o software deve ser estruturado em alto nível — estilos arquiteturais, fronteiras, camadas e padrões.
> **Como a IA deve usar:** ao desenhar a estrutura de um projeto novo ou refatorar, siga estas preferências antes de aplicar defaults. Justifique qualquer desvio.

---

## Estilo arquitetural preferido

- **Clean Architecture** como base, organizada em torno de **Use Cases** (casos de uso) explícitos.
- A regra de dependência aponta sempre para dentro: domínio no centro, sem conhecer infraestrutura, frameworks ou detalhes de entrega.
- Cada caso de uso é uma unidade de orquestração própria (uma intenção de negócio = um use case), com entrada e saída bem definidas.

## Domínio (DDD)

- Modelagem orientada a **Domain-Driven Design**.
- Domínio rico: regras de negócio vivem em entidades, agregados e objetos de valor — não em serviços anêmicos nem em controllers.
- Linguagem ubíqua refletida nos nomes de classes, métodos e pacotes.
- Fronteiras de contexto explícitas quando o domínio crescer.

## Organização de camadas e fronteiras

- Separação clara entre **domínio**, **aplicação (use cases)**, **infraestrutura** e **interface/entrega**.
- Domínio e aplicação não dependem de Spring, banco, HTTP ou qualquer detalhe externo — esses ficam na borda (adapters).
- Inversão de dependência via portas/interfaces definidas pelas camadas internas.

## Tratamento de erros

- Tratamento de erros é requisito de primeira classe, não um `try/catch` improvisado.
- Erros de domínio modelados explicitamente (exceções de negócio próprias), distintos de falhas técnicas/infraestrutura.
- Falhas devem ser propagadas com contexto suficiente para rastreio (ver `05-observabilidade.md` — todo erro relevante vira log funcional).
- Nada de engolir exceção silenciosamente.

## Resiliência (circuit breaker, timeout, retry)

- **Java/Spring Boot:** usar **Resilience4j** (starter oficial do Spring Boot) em toda integração externa.
  - **Timeout** de leitura padrão: ~5s.
  - **Circuit breaker:** janela deslizante, abertura em **50%** de falha, `wait-duration-in-open-state` de **10s**.
  - **Retry:** até **3 tentativas** com backoff exponencial + jitter, **somente em operações idempotentes**.
- **Lambdas Python:** **não usam circuit breaker** (execução curta e isolada). Resiliência via **timeout explícito + retry** na configuração do cliente AWS (`botocore`) ou `tenacity` quando necessário.

## Decisões em aberto

> Nenhuma no momento.
