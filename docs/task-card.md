# Especificação do card de tarefa

Este documento é a fonte de verdade para criar e manter cards exibidos em `BOARD.base`.

## Armazenamento

Cada card é uma pasta dentro de `tasks/`. A nota principal tem o mesmo nome da pasta:

```text
tasks/<título-do-card>/
├── <título-do-card>.md
└── attachments/
```

Crie `attachments/` somente quando houver um anexo. O filtro `file.inFolder("tasks")` do board inclui as subpastas dos cards e exclui os próprios anexos dos resultados.

Use um título curto e específico. Em nomes de pasta e arquivo, remova caracteres inválidos no Windows. Antes de criar, procure títulos semelhantes para evitar duplicidade e confirme que o destino não existe.

## Identidade

Todo card possui um `id` imutável com oito caracteres hexadecimais minúsculos, por exemplo `7ac31f92`. Gere o valor aleatoriamente, confirme que ele é único entre os cards existentes e gere outro em caso de colisão.

O título pode mudar; o `id` permanece. O usuário pode referenciar um card pelo ID completo ou por um prefixo que identifique somente um card.

## Estados

O frontmatter aceita somente estes valores de `status`:

| Valor persistido | Significado |
| --- | --- |
| `To Do` | A fazer |
| `In Progress` | Fazendo |
| `Done` | Feito |
| `Cancelled` | Cancelado |

Novos cards começam em `To Do`, salvo quando o usuário pedir explicitamente outro estado. O Base Board pode adicionar `kanban_order`; preserve esse campo quando existir e deixe a ordenação a cargo do plugin.

## Formato

Todo card segue esta estrutura:

```markdown
---
id: 7ac31f92
status: To Do
tags: []
---

## Objetivo

<resultado que a tarefa deve produzir>

## Contexto

<informações necessárias para executar a tarefa>

## Critérios de aceitação

- [ ] <resultado observável>

## Resultado

<preencher ao concluir ou cancelar>

## Notas

<decisões, descobertas e acompanhamento>

## Anexos

<links para arquivos em attachments/>
```

`id`, `status` e `tags` são propriedades obrigatórias. Mantenha `tags` como lista YAML, preserve propriedades adicionais existentes e nunca altere o `id` de um card. Preencha as seções com fatos disponíveis e critérios verificáveis; deixe uma seção vazia quando não houver informação real.

## Localização de cards existentes

Antes de alterar, mover ou anexar arquivos, pesquise todas as notas Markdown sob `tasks/` e resolva a referência nesta ordem:

1. ID exato ou prefixo único do ID.
2. Título exato da pasta ou da nota.
3. Trecho de título que corresponda a somente um card.
4. Correspondência inequívoca por tags e conteúdo.

Quando houver mais de um candidato plausível, apresente uma lista curta com ID, título e status e aguarde a escolha do usuário. Quando nenhum card corresponder, informe isso; crie um card somente quando o pedido for de criação.

## Operações

### Criar

1. Derive o título e verifique possíveis duplicatas.
2. Gere um `id` único no formato definido neste contrato.
3. Crie a pasta do card e a nota com o mesmo nome.
4. Preencha o formato completo e defina um estado aceito.
5. Confirme que o Markdown está sob `tasks/` e satisfaz o filtro do board.

### Editar ou mover

- Preserve conteúdo e propriedades não relacionados ao pedido.
- Para mover, altere `status` e preserve `kanban_order`.
- Ao renomear, renomeie pasta e nota juntas e atualize os links internos afetados.
- Use `Done` após satisfazer os critérios de aceitação; marque os checkboxes e registre o resultado.
- Use `Cancelled` com o motivo registrado em `Resultado`.

### Anexar

1. Crie `<pasta-do-card>/attachments/` quando necessário.
2. Salve o arquivo com nome legível, preservando anexos existentes.
3. Adicione em `Anexos` um link relativo do Obsidian, por exemplo `![[attachments/evidencia.png]]`.

## Verificação final

Antes de concluir uma operação, confirme que o caminho, o frontmatter, as seções obrigatórias, os links de anexos e o estado resultante obedecem a este contrato. Informe ao usuário o caminho do card e seu estado. Commit e push exigem solicitação explícita.
