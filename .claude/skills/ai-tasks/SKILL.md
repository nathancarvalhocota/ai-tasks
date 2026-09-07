---
name: ai-tasks
description: Gerencie tarefas no vault AI Tasks configurado.
argument-hint: "[pedido sobre tarefas]"
disable-model-invocation: true
---

# AI Tasks

## Localize o vault

Considere válido um diretório que contenha `Tasks.base`, `Tasks/` e `docs/task-card.md`.

1. Use o diretório atual ou um de seus ancestrais quando ele for um vault válido.
2. Caso contrário, leia `~/.ai-tasks/config.json` e use o caminho absoluto da propriedade `vault`.
3. Se a configuração estiver ausente ou inválida, solicite o caminho do vault, valide-o e grave `{"vault":"<caminho-absoluto>"}` nesse arquivo.
4. Evite procurar o vault pelo disco inteiro.

Quando a skill for executada dentro de um vault válido diferente do configurado, use o vault atual e atualize a configuração local.

## Execute o pedido

Leia integralmente `<vault>/docs/task-card.md`. Interprete o pedido em linguagem natural, opere somente os arquivos necessários sob `<vault>/Tasks/` e aplique a verificação final do contrato.

O Obsidian e seu CLI são opcionais. Relate os cards encontrados ou alterados, incluindo caminho, ID e estado. Faça commit ou push somente quando o usuário pedir explicitamente.
