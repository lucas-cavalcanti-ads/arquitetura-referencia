# 13 — Colaboração com IA

> **Propósito:** definir **como** um agente de IA deve trabalhar com o Lucas — o processo, não o código.
> **Como a IA deve usar:** estas são regras de conduta da colaboração. Valem em conjunto com os demais arquivos (que dizem *o que* construir).

---

## Estilo de comunicação

- **Idioma:** Português (Brasil), direto e conciso.
- O Lucas costuma dar **restrições duras** e delegar os tradeoffs à IA. A IA **decide o caminho**, aplica um default razoável e **sinaliza a decisão/suposição** — sem ficar devolvendo lista de opções quando o rumo já foi dado.
- Quando houver lacuna nas preferências, assumir um default sensato e sinalizar, em vez de travar.

## Fluxo de trabalho: spec antes de codar

- Para qualquer **tarefa não-trivial**, a IA **escreve uma spec/plano e espera o OK do Lucas antes de implementar**.
- A spec deve conter, no mínimo:
  - **Objetivo** — o que se quer alcançar.
  - **Escopo** — o que entra e o que fica de fora.
  - **Pré-condições** — o que precisa estar verdadeiro para começar.
  - **Passos de execução** — o plano em etapas.
  - **Pós-condições / Definição de pronto** — como saber que terminou.
  - **Riscos / o que pode falhar** — e o plano se falhar.
- Tarefas triviais (ajuste pontual, correção óbvia) dispensam spec formal.

## Progresso em passos com checkpoints

- Tarefas longas são entregues **em passos, com checkpoints** — pontos de verificação onde o Lucas confere e corrige o rumo antes de seguir.
- Não sumir e voltar só com o resultado final de algo grande.

## Autonomia e ações com efeito colateral

| Ação | Conduta |
|---|---|
| **Commit e push** | **Permitido** sem confirmar (dispara o CI — ver `06-ci-cd-e-deploy.md`). |
| **Deploy** | **Nunca manual pela IA** — deploy acontece **exclusivamente pela esteira** (GitHub Actions). |
| **`terraform apply` em recursos reais / AWS** | **Confirmar antes.** |
| **Apagar dados, recursos ou arquivos** | **Confirmar antes.** |
| **Qualquer ação irreversível ou com custo** | **Confirmar antes.** |

## Definição de "pronto" (checklist do agente)

Antes de declarar uma tarefa concluída, a IA garante:

- Testes passando e **cobertura ≥ 95% por módulo** (ver `03-qualidade-e-testes.md`).
- **CI verde** (ver `06-ci-cd-e-deploy.md`).
- **README** criado/atualizado (ver `08-governanca-e-documentacao.md`).
- Tudo em **Português (Brasil)**.
- Nenhum segredo no repositório (ver `09-seguranca-e-segredos.md`).

## Como navegar a arquitetura de referência

1. Ler o `README.md` desta pasta primeiro.
2. Abrir os arquivos do(s) tema(s) da tarefa.
3. Respeitar a precedência: instrução direta na conversa > regra do projeto > arquitetura de referência > defaults.
4. Sinalizar lacunas e suposições.

## Decisões em aberto

> Nenhuma no momento.
