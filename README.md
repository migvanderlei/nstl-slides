# nstl-slides

Repositório para **apresentações em HTML** com [Reveal.js](https://revealjs.com/): cada palestra ou versão fica em sua própria pasta, tudo versionável e fácil de hospedar como site estático.

---

## Por que existe

- **Slides autocontidos** — HTML + opcional `assets/`; Reveal via CDN (jsDelivr), sem build obrigatório.  
- **Vários decks** — Um diretório por tema ou evento, sem misturar conteúdo.  
- **Skill no Cursor** — Fluxo guiado (entrevista → sumário → aprovação → tema → arquivo final); conteúdo dos slides em **português do Brasil** por padrão.

---

## Estrutura

```
nstl-slides/
├── README.md                 ← você está aqui
├── decks/
│   ├── README.md             ← índice dos decks
│   ├── _template/            ← copie para começar um deck novo
│   └── sample-welcome/       ← exemplo mínimo (pode apagar)
└── .cursor/skills/html-slides/
    ├── SKILL.md              ← instruções da skill
    └── reference.md          ← Reveal, tema, PDF, etc.
```

Convensão de nome para pastas em `decks/`: minúsculas, hífens, opcionalmente data ou evento (ex.: `tech-day-2026-04`).

---

## Ver os slides no computador

Na raiz do repositório:

```bash
python3 -m http.server 8000
```

Abra no navegador (note a **barra no final** do caminho):

`http://localhost:8000/decks/sample-welcome/`

Para um deck que você criou: `http://localhost:8000/decks/<nome-da-pasta>/`

Um único `index.html` também pode ser aberto via `file://`, mas um servidor local evita surpresas com caminhos e alguns plugins.

---

## Publicar (opcional)

Qualquer hospedagem estática serve (GitHub Pages, Netlify, Cloudflare Pages, etc.). Publique a raiz do repositório para manter URLs do tipo `/decks/<slug>/`.

Repositório no GitHub: [github.com/migvanderlei/nstl-slides](https://github.com/migvanderlei/nstl-slides)

---

## Skill do Cursor: `html-slides`

A skill ensina o agente a **montar o deck com você**, não a “chutar” 40 slides de uma vez.

### O que ela faz

1. **Entrevista** — Público, objetivo, duração, o que não pode faltar, tom, fechamento.  
2. **Sumário (TOC)** — Lista numerada: título do slide + uma linha do propósito.  
3. **Aprovação** — Só depois do seu “ok” (ou ajustes) ela gera o HTML.  
4. **Estilo** — Modo claro/escuro, cores, tipografia, densidade, movimento; aplica no tema Reveal.  
5. **Entrega** — Um `index.html` standalone, em **pt-BR** por padrão (`lang="pt-BR"`).

Detalhes técnicos (Reveal, variáveis CSS `--r-*`, PDF, fallback sem CDN) estão em `.cursor/skills/html-slides/reference.md`.

### Como usar no Cursor

1. **Clone** este repositório (a pasta `.cursor/skills/` vai junto).  
2. Abra a **raiz** do projeto no Cursor.  
3. Para o agente seguir a skill, **anexe** a skill à mensagem (anexo manual da skill *html-slides*, se o seu Cursor listar skills do projeto) **ou** escreva algo como: *“Use a skill html-slides e crie um deck sobre …”*.  
4. Responda às perguntas, **aprove o sumário**, defina o visual — só então peça o arquivo.

Se a skill não aparecer automaticamente, confira se o diretório `.cursor/skills/html-slides/SKILL.md` existe na raiz do workspace.

### Onde editar a skill

| Arquivo | Função |
|---------|--------|
| `.cursor/skills/html-slides/SKILL.md` | Fluxo, regras, checklist |
| `.cursor/skills/html-slides/reference.md` | Referência técnica (Reveal, tema, PDF) |

---

## Novo deck rapidamente

```bash
cp -r decks/_template decks/meu-assunto
# edite decks/meu-assunto/index.html
```

Atualize também `decks/README.md` com uma linha no índice. Mais detalhes: [decks/README.md](decks/README.md).
