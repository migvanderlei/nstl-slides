# Decks

Cada subpasta aqui é **um deck independente**: em geral um `index.html` e, se precisar, uma pasta `assets/` (imagens, fontes locais, etc.).

---

## Índice

| Pasta | Descrição |
|-------|-----------|
| `_template/` | Ponto de partida: **copie a pasta inteira**, renomeie (ex.: `onboarding-produto`) e edite o `index.html`. Não use `_template/` como deck “oficial”. |
| `sample-welcome/` | Exemplo mínimo para abrir no navegador e ver o fluxo; pode remover quando não precisar mais. |

Quando criar um deck novo, **adicione uma linha** na tabela acima para quem clonar o repo saber o que existe.

---

## Criar um deck novo

1. Duplicar o template:

   ```bash
   cp -r decks/_template decks/nome-do-seu-deck
   ```

2. Ajustar título no `<title>` e o conteúdo dentro de `<div class="slides">` no `index.html`.  
3. Colocar mídia em `decks/nome-do-seu-deck/assets/` e referenciar com caminhos relativos.  
4. Abrir `decks/nome-do-seu-deck/index.html` no navegador para testar.

Scripts e estilos do Reveal vêm da CDN; não é obrigatório Node/npm para editar slides simples.

---

## Convenções

- **Nome da pasta**: minúsculas, sem espaços, hífens em vez de underscore (ex.: `meetup-sp-2026`).  
- **Um assunto por pasta**; variante grande de palestra = nova pasta ou novo `index.html` na mesma pasta, o que fizer mais sentido para você.  
- Manter cada deck **autocontido** facilita GitHub Pages e links diretos.
