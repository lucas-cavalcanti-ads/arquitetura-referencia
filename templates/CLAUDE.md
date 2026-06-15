# CLAUDE.md

> Template de ponto de entrada por projeto. Copie este arquivo para a **raiz** do repositório do projeto e preencha a seção "Específico deste projeto".
> O Claude Code lê este arquivo automaticamente ao abrir o projeto.

---

## Arquitetura de Referência (regras globais)

Este projeto segue a **Arquitetura de Referência**:
`https://github.com/<OWNER>/arquitetura-referencia`

Antes de construir, revisar ou propor software:

1. Leia o `README.md` da arquitetura de referência (índice) e abra os arquivos `NN-*.md` do tema da tarefa.
2. Trate aquelas regras como **preferência autoritativa**. Precedência: instrução direta na conversa > regras específicas deste projeto (abaixo) > arquitetura de referência > defaults.
3. Pontos não-negociáveis (resumo — a fonte é o repositório):
   - **Stack:** Java 21 + Maven; Python 3.13 (Lambdas); Spring Boot quando REST.
   - **Arquitetura:** Clean Architecture + Use Cases, DDD; Resilience4j em integrações.
   - **Testes:** cobertura ≥ 95% por módulo; Testcontainers em integração.
   - **Local sempre:** todo sistema roda 100% local (LocalStack + Docker).
   - **CI/CD:** GitHub Actions; feature branches → `main`; PR automático quando CI passa; deploy só pela esteira.
   - **Observabilidade:** logs JSON estruturados (id, mensagem, horário, nível, correlationId); não logar PII.
   - **Segredos:** nunca no repositório.
   - **Idioma:** todos os artefatos em Português (Brasil).
   - **Fluxo com IA:** spec antes de tarefa não-trivial (aguardar OK); commit/push liberados; entregas longas em checkpoints. Ações irreversíveis/custosas pedem confirmação.

> Para fixar uma versão específica das regras, referencie uma tag: `.../arquitetura-referencia/tree/v1.0.0`.

---

## Específico deste projeto

- **Domínio / objetivo:** _descrever_
- **Módulos principais:** _descrever_
- **Comandos úteis:** _build, testes, subir ambiente local_
- **Exceções às regras globais (se houver):** _justificar_
