---
name: ai-tasks
description: Gerencie tarefas no vault AI Tasks associado ao diretório atual.
---

# AI Tasks

## Resolva o vault

Considere válido um diretório que contenha `BOARD.base`, `tasks/` e `docs/task-card.md`.

1. Preserve o diretório em que a skill foi invocada como origem da resolução.
2. Se o usuário informar um caminho de vault, valide o diretório exato e use-o.
3. Se a origem ou um de seus ancestrais for um vault válido, use o mais próximo.
4. Caso contrário, percorra a origem e seus ancestrais em direção à raiz. Em cada nível, examine somente o filho direto `ai-tasks`; use o primeiro que for um vault válido.
5. Se nenhum candidato for válido, encerre antes de alterar arquivos e peça que o usuário execute o agente dentro de um escopo que contenha `ai-tasks` ou forneça o caminho exato.

Limite a descoberta aos caminhos descritos. Uma execução em um diretório pai não alcança vaults dentro de outros descendentes ou irmãos.

## Encaminhe o pedido

- Para criar, localizar, editar, mover ou anexar tarefas, leia integralmente `<vault>/docs/task-card.md`, opere somente os arquivos necessários sob `<vault>/tasks/` e aplique a verificação final do contrato.
- Para atualizar a estrutura do vault a partir do repositório público, leia integralmente `<vault>/docs/update.md` e siga seu procedimento.

O Obsidian e seu CLI são opcionais. Relate os cards encontrados ou alterados, incluindo caminho, ID e estado. Faça commit ou push somente quando o usuário pedir explicitamente.
