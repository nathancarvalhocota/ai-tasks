# Atualização segura do vault

Use este procedimento somente quando o usuário pedir para atualizar um vault a partir do projeto público. Os arquivos em `tasks/` são dados do usuário e permanecem preservados durante toda a operação.

## Preparação

1. Confirme que o diretório resolvido é um vault válido e um repositório Git.
2. Execute `git status --short --branch` e verifique se existe merge ou rebase em andamento.
3. Se houver alterações não commitadas, apresente-as e peça ao usuário que escolha entre criar um commit local, guardar as alterações com stash ou cancelar. Commit e stash exigem autorização explícita; descarte nunca é uma opção de atualização.
4. Use `upstream` quando esse remote apontar para `nathancarvalhocota/ai-tasks`; caso contrário, use `origin` se ele apontar para esse repositório. Aceite URLs GitHub HTTPS ou SSH. Se nenhum deles corresponder, peça confirmação antes de adicionar ou alterar remotes.

Continue quando o índice e a árvore de trabalho estiverem limpos e nenhuma operação Git estiver em andamento.

## Integração

1. Execute `git fetch <remote> main`.
2. Se `HEAD` já contiver `<remote>/main`, informe que o vault está atualizado.
3. Se `HEAD` for ancestral de `<remote>/main`, execute `git merge --ff-only <remote>/main`.
4. Se as histórias tiverem divergido por commits locais, execute `git merge --no-edit <remote>/main`.
5. Se houver conflito, preserve o estado anterior com `git merge --abort`, liste os caminhos conflitantes e encerre sem escolher versões automaticamente.

## Verificação

Confirme que `BOARD.base`, `tasks/` e `docs/task-card.md` existem, que `git status` não contém conflitos e que todo o conteúdo anterior de `tasks/` permanece presente. Informe os commits integrados e qualquer ação manual ainda necessária.

Quando a atualização modificar a distribuição da skill usada pelo agente, sincronize `<vault>/.agents/skills/ai-tasks/` para Codex ou `<vault>/.claude/skills/ai-tasks/` para Claude Code e informe que o agente deve ser reiniciado. Escrever fora do vault exige a autorização aplicável do ambiente.
