# Guia de operação para agentes

AI Tasks é um vault Obsidian local-first. Markdown e anexos são a fonte de verdade; não há aplicação, API ou banco de dados.

## Antes de operar tarefas

- Quando o usuário invocar `ai-tasks`, localize o vault conforme a própria skill e cumpra o pedido em linguagem natural.
- Consulte `BOARD.base` para confirmar os estados aceitos e o diretório filtrado pelo board.
- Trate [`docs/task-card.md`](docs/task-card.md) como a fonte de verdade do formato e do fluxo dos cards.
- Para atualizar um vault com mudanças do projeto público, siga [`docs/update.md`](docs/update.md).

## Limites estruturais

- Preserve as quatro colunas existentes e seus valores de `status`.
- Preserve o filtro do board e a organização de uma pasta por card.
- Em mudanças estruturais do projeto, trate `tasks/` como dados do usuário e preserve todo o seu conteúdo.
- Trate `kanban_order` como metadado gerenciado pelo Base Board: preserve-o quando existir.
- Mantenha alterações de conteúdo fora de `.obsidian/plugins/`; esses arquivos pertencem aos plugins instalados.
- Edite configurações do Obsidian ou do board somente quando o pedido exigir essa mudança.

## Manutenção da skill

- `.agents/skills/ai-tasks/` e `.claude/skills/ai-tasks/` são distribuições da mesma skill para agentes diferentes.
- Mantenha o comportamento das duas distribuições equivalente e preserve apenas os metadados específicos de cada agente.
- Mantenha o contrato dos cards em `docs/task-card.md`; a skill deve apontar para ele em vez de duplicá-lo.

## Git

Mantenha cada alteração restrita às tarefas e documentações solicitadas. Faça commit ou push somente quando o usuário pedir explicitamente.
