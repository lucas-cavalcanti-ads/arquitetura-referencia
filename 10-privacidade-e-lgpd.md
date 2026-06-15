# 10 — Privacidade e LGPD

> **Propósito:** garantir tratamento adequado de dados pessoais conforme a LGPD.
> **Como a IA deve usar:** ao lidar com dados que identifiquem pessoas, aplicar estes princípios por padrão.

---

## Identificação de dados pessoais

- Identificar e marcar quais campos são **dados pessoais / PII** (nome, CPF, e-mail, telefone, dados financeiros, etc.).
- Tratar dado pessoal sensível (financeiro, por exemplo) com cuidado redobrado.

## Princípios aplicados

- **Minimização:** coletar e armazenar apenas o dado necessário para a finalidade.
- **Finalidade e base legal:** todo tratamento deve ter finalidade clara e base legal (consentimento, execução de contrato, obrigação legal, etc.).
- **Retenção:** definir por quanto tempo o dado é mantido; não guardar indefinidamente.

## Proteção do dado

- **Não logar PII** — mascarar/ocultar em logs (conecta com `05-observabilidade.md`, onde o log "conta toda a história" mas não pode vazar dado pessoal).
- **Criptografia:** em trânsito (TLS) e em repouso (criptografia do RDS/S3 na AWS).
- Acesso a dado pessoal restrito ao mínimo necessário.

## Direitos do titular

- Prever que o titular pode solicitar acesso, correção e exclusão dos próprios dados; a modelagem deve permitir localizar e remover dados de uma pessoa.

## Decisões em aberto

> _A preencher quando houver um caso concreto: catálogo dos dados pessoais tratados por aplicação, política de retenção específica e fluxo de atendimento a solicitações do titular._
