# Curso Open Design — 3 Trilhas (formato INEMA.CLUB)

## Contexto

Open Design (OD) é a alternativa open-source ao [Claude Design][cd] da Anthropic — um produto que viralizou em abril/2026 ao mostrar que LLMs podiam parar de escrever prosa e começar a entregar artefatos de design HTML rodáveis. Mas o Claude Design é fechado, pago, na nuvem, preso ao Anthropic. O OD é local-first, BYOK em todas as camadas, e usa **a CLI de agente que já está no laptop do usuário** (Claude Code, Codex, Cursor, Gemini, etc.) como motor de design — conduzida por **31 skills componíveis** (`SKILL.md`) e **72 design systems** (`DESIGN.md`).

O usuário pediu um curso profundo sobre OD em **3 trilhas** (Fundamentos · Exemplos de Uso · Técnicas Avançadas), seguindo o formato INEMA.CLUB que ele já usa em outros cursos. O curso precisa ser conteúdo denso de verdade — não panorama superficial — porque o OD não é um produto raso: ele empilha 6+ tradições (huashu-design, guizang-ppt, open-codesign, multica, awesome-claude-design, Claude Code skills) numa stack de prompts componível que é o **produto real** (não a UI). Aprender OD bem significa aprender:

1. **Filosofia de design** (anti-AI-slop, junior-designer mode, 5-dim critique, brand-spec extraction)
2. **Engenharia de prompt-stack** (composição de camadas: discovery + identity + DESIGN + SKILL + metadata)
3. **Arquitetura local-first** (daemon, sidecar IPC, BYOK proxy, ACP, agent adapters, multi-CLI dispatch)

**Decisões fechadas com o usuário:**
- **Local:** `/home/nmaldaner/projetos/curso-od/`
- **Audiência:** híbrida (designer-engineer) — Trilha 1 cobre os dois; T2 puxa pro uso; T3 puxa pra arquitetura/extensibilidade
- **Tamanho:** 6 módulos por trilha (18 módulos no total, 6+ tópicos por módulo = 100+ tópicos)
- **Idioma:** Português (BR)
- **Formato:** INEMA.CLUB (skill `formato-curso`) — Tailwind via CDN, dark/light, navegação global, INEMA.CLUB link, light-mode CSS completo, tópicos numerados em círculo, 3 seções por tópico (O que é / Por que aprender / Conceitos-chave)

---

## Arquitetura do Curso

```
/home/nmaldaner/projetos/curso-od/
├── index.html                          ← Landing do curso (pitch + 3 trilhas)
└── curso/
    ├── trilha1-fundamentos/            ← cor emerald (T1)
    │   ├── index.html                  ← cards de 6 módulos + tópicos expansíveis
    │   ├── modulo-1-1.html             ← Por que Open Design existe
    │   ├── modulo-1-2.html             ← Arquitetura mental
    │   ├── modulo-1-3.html             ← O Stack de Prompts é o Produto
    │   ├── modulo-1-4.html             ← Skills (SKILL.md)
    │   ├── modulo-1-5.html             ← Design Systems (DESIGN.md)
    │   └── modulo-1-6.html             ← Junior-Designer Mode
    ├── trilha2-exemplos/               ← cor blue (T2)
    │   ├── index.html
    │   ├── modulo-2-1.html             ← Pitch Deck (guizang-ppt)
    │   ├── modulo-2-2.html             ← Landing Page SaaS
    │   ├── modulo-2-3.html             ← App Mobile Multi-tela
    │   ├── modulo-2-4.html             ← Carrossel Social
    │   ├── modulo-2-5.html             ← Dashboard / Tool UI
    │   └── modulo-2-6.html             ← Crítica & Tweaks
    └── trilha3-avancado/               ← cor purple (T3)
        ├── index.html
        ├── modulo-3-1.html             ← BYOK Proxy & Multi-modelo
        ├── modulo-3-2.html             ← Agent Client Protocol (ACP) & adapters
        ├── modulo-3-3.html             ← Brand-Spec Extraction Avançada
        ├── modulo-3-4.html             ← Critique 5-dim como Loop
        ├── modulo-3-5.html             ← Criando uma Skill Própria
        └── modulo-3-6.html             ← Daemon, Sidecar IPC & Multi-namespace
```

**Total:** 1 landing + 3 índices de trilha + 18 módulos = **22 páginas HTML**

---

## Trilha 1 — Fundamentos (emerald)

> **Objetivo:** Construir o modelo mental sólido do OD. Ao final, o aluno entende **por que** o OD existe, **como** ele pensa, e **quais** são as peças que se combinam.

### Módulo 1.1 · Por que Open Design existe

**Resultado de aprendizagem:** O aluno consegue articular o problema que o OD resolve em 30 segundos, e diferenciá-lo de Claude Design, Figma AI, V0.dev e ferramentas de "AI freestyle".

**Tópicos (mínimo 6):**
1. **O viral do Claude Design (abril/2026)** — o que ele provou e o que ele trava
2. **O problema do "AI freestyle"** — por que prompts longos não bastam
3. **Anti-AI-slop como tese** — o que conta como slop (gradiente roxo, emoji icons, métricas inventadas...)
4. **Local-first como princípio** — daemon, sem nuvem obrigatória, BYOK em toda camada
5. **A CLI que já está no laptop** — agentes como motores plugáveis, não como dependência
6. **Quatro ombros open-source** — huashu-design, guizang-ppt, open-codesign, multica (linhagem)
7. **Comparação: Claude Design vs Open CoDesign vs Open Design** — eixos de licença, deploy, runtime, skill

**Fontes no repo:** `README.md`, `docs/spec.md`, `docs/references.md`

---

### Módulo 1.2 · Arquitetura mental do OD

**Resultado de aprendizagem:** O aluno desenha de cabeça o data-flow: chat → skill picker → design-system picker → daemon → CLI → `<artifact>` → iframe preview, e sabe onde cada peça é editável.

**Tópicos:**
1. **As 5 peças que se combinam** — chat, skill, design system, agent CLI, iframe preview
2. **As 3 topologias de deploy** — A (totalmente local), B (Vercel + tunnel), C (browser-only API direct)
3. **Daemon vs Web vs Desktop** — quem é responsável por o quê
4. **`<artifact>` parser e srcdoc iframe** — o ciclo de render seguro
5. **SQLite local: projetos, conversas, mensagens, abas, templates** — `.od/app.sqlite`
6. **Importação de ZIP do Claude Design** — `POST /api/import/claude-design`

**Fontes no repo:** `docs/architecture.md` §1-§3, `apps/daemon/src/server.ts`, `apps/web/src/artifacts/parser.ts`

---

### Módulo 1.3 · O Stack de Prompts é o Produto

**Resultado de aprendizagem:** O aluno entende que **a UI não é o produto** — o produto é a stack de prompts componível. Sabe ler `system.ts`, `discovery.ts`, `directions.ts` e modificar uma camada sem quebrar as outras.

**Tópicos:**
1. **As 6 camadas da stack** — discovery + identity charter + DESIGN + SKILL + project metadata + skill side-files + (deck framework)
2. **Por que componível** — cada camada é um arquivo, cada arquivo é editável
3. **DISCOVERY directives — RULES 1, 2, 3** — turn 1 form → turn 2 brand branch → TodoWrite
4. **Identity charter (OFFICIAL_DESIGNER_PROMPT)** — anti-slop fixo, junior-pass
5. **Pre-flight de side-files** — auto-injeção de `assets/template.html` + `references/*.md`
6. **Override hierarchy** — discovery domina sobre identity; metadata adapta

**Fontes no repo:** `packages/contracts/src/prompts/system.ts`, `packages/contracts/src/prompts/discovery.ts` (263 linhas), `packages/contracts/src/prompts/official-system.ts`

---

### Módulo 1.4 · Skills (SKILL.md) — a unidade atômica

**Resultado de aprendizagem:** O aluno lê uma SKILL.md e prevê o comportamento do agente. Sabe a diferença entre skill base (Claude Code-compatível) e skill com extensão `od:`.

**Tópicos:**
1. **Convenção `SKILL.md` do Claude Code** — frontmatter mínimo (name, description, triggers)
2. **Anatomia: `assets/` + `references/`** — o que vai em cada um
3. **Extensão `od:` no frontmatter** — mode, platform, scenario, preview, design_system, default_for, featured
4. **As 31 skills da box** — taxonomia (prototype × deck × scenario)
5. **Pre-flight reading enforcement** — por que o agente lê `template.html` antes de escrever CSS
6. **Promessa de compatibilidade** — uma skill OD roda em Claude Code puro, e vice-versa
7. **Onde skills moram** — `~/.claude/skills/`, `./skills/`, `./.claude/skills/` (escaneadas no boot)

**Fontes no repo:** `docs/skills-protocol.md` (322 linhas), `skills/web-prototype/SKILL.md`, `skills/guizang-ppt/SKILL.md`, `apps/daemon/src/skills.ts`

---

### Módulo 1.5 · Design Systems (DESIGN.md) — o vocabulário visual

**Resultado de aprendizagem:** O aluno escreve um `DESIGN.md` válido para uma marca real, em OKLch, e sabe escolher quando usar um sistema do catálogo vs. criar um novo.

**Tópicos:**
1. **O schema de 9 seções** — color, typography, spacing, layout, components, motion, voice, brand, anti-patterns
2. **Por que OKLch e não HSL/HEX** — uniformidade perceptual, Display P3, predictabilidade WCAG
3. **Os 72 sistemas de produto** — taxonomia (AI/LLM, dev tools, productivity, fintech, e-commerce, media, automotive)
4. **Tokens compartilhados: `--bg`, `--surface`, `--fg`, `--muted`, `--border`, `--accent`** — vínculo no `:root`
5. **Como o agente lê DESIGN.md ao gerar** — pruning de seções via `design_system.sections`
6. **Importar do upstream** — `scripts/sync-design-systems.ts` puxando de `awesome-design-md`
7. **Quando criar um sistema novo** — vs. estender um existente

**Fontes no repo:** `design-systems/README.md`, `design-systems/linear-app/DESIGN.md` (exemplo canônico), `scripts/sync-design-systems.ts`. Externa: [evilmartians.com/chronicles/oklch-in-css](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl)

---

### Módulo 1.6 · Junior-Designer Mode — a filosofia que evita 80% dos retrabalhos

**Resultado de aprendizagem:** O aluno aplica o protocolo de descoberta antes de qualquer pixel: question form → branch de marca → 5 direções visuais → TodoWrite → execução → checklist P0 → crítica 5-dim.

**Tópicos:**
1. **A herança do `huashu-design`** — designer júnior simula sênior batendo perguntas
2. **RULE 1: question form no turn 1** — superfície, audiência, tom, contexto de marca, escala
3. **RULE 2 — branch de marca** — A (escolha direção), B (extração de brand-spec), C (improvisar)
4. **As 5 direções visuais** — Editorial Monocle, Modern Minimal, Tech Utility, Brutalist, Soft Warm
5. **RULE 3: TodoWrite + live updates** — plano visível, redirecionável
6. **P0/P1/P2 checklist** — gate pre-emit
7. **Crítica 5-dim** — Philosophy / Hierarchy / Execution / Specificity / Restraint
8. **"Variations, not the answer"** — 2-3 direções diferenciadas quando o usuário explora

**Fontes no repo:** `packages/contracts/src/prompts/discovery.ts` (263 linhas — leitura obrigatória), `packages/contracts/src/prompts/directions.ts` (284 linhas), `skills/critique/SKILL.md`, `skills/tweaks/SKILL.md`. Externa: [github.com/alchaincyf/huashu-design](https://github.com/alchaincyf/huashu-design)

---

## Trilha 2 — Exemplos de Uso (blue)

> **Objetivo:** Para cada formato real (deck, landing, mobile, carrossel, dashboard, crítica), mostrar o fluxo completo: brief → form → direction → todos → artefato → autocrítica → export.

### Módulo 2.1 · Pitch Deck com guizang-ppt

**Resultado de aprendizagem:** O aluno gera um pitch deck rodada-seed estilo Monocle/FT em ~10 minutos. Domina theme rhythm, slide counter, escala-fit-tela.

**Tópicos:**
1. **Por que o `guizang-ppt-skill` é default para deck** — magazine-style web PPT
2. **A estrutura: `assets/template.html` + `references/{themes,layouts,components,checklist}.md`**
3. **WebGL hero backgrounds — quando usar e quando evitar**
4. **Theme rhythm: nunca 3+ slides do mesmo tema seguidos**
5. **Slide counter, navegação, persistência em localStorage**
6. **Export: HTML único + PDF (impressão deck-aware)**
7. **Speaker notes — quando incluir e como o agente decide**

**Hands-on:** Brief = "10 slides para apresentar um SaaS de gestão financeira para investidores anjo brasileiros". Output esperado: HTML rodável, PDF imprimível, speaker notes.

**Fontes no repo:** `skills/guizang-ppt/SKILL.md`, `skills/guizang-ppt/assets/template.html`, `skills/guizang-ppt/references/checklist.md`, `templates/deck-framework.html`

---

### Módulo 2.2 · Landing Page SaaS

**Resultado de aprendizagem:** O aluno gera uma landing com hero/features/pricing/CTA usando direção visual coerente com a marca.

**Tópicos:**
1. **`saas-landing` skill — anatomia**
2. **As 8 seções da `references/layouts.md`** — hero, features, pricing, social proof, testimonials, FAQ, CTA, footer
3. **Rítmo padrão: hero → 3 features → social proof → pricing → CTA**
4. **One decisive flourish** — uma imagem real, um pull-quote, ou uma animação de carga (escolher uma)
5. **Pricing table — 3 colunas, "highlight da do meio"**
6. **Trust signals honestos vs. invented metrics** — como o agente lida quando não tem números reais
7. **Responsividade: viewport, breakpoints, touch targets**

**Hands-on:** Brief = "landing para um curso online de Cybersegurança para devs". Output: index.html responsivo + pricing/3 planos + FAQ acordeão.

**Fontes no repo:** `skills/saas-landing/SKILL.md`, `skills/saas-landing/references/layouts.md`

---

### Módulo 2.3 · App Mobile Multi-tela

**Resultado de aprendizagem:** O aluno produz protótipo mobile pixel-accurate (iPhone 15 Pro Dynamic Island), com 3+ telas usando frames compartilhados.

**Tópicos:**
1. **`mobile-app` vs `mobile-onboarding` vs `gamified-app`** — quando cada um
2. **Os 5 frames compartilhados em `/frames/`** — iphone-15-pro, android-pixel, ipad-pro, macbook, browser-chrome
3. **Padrão multi-tela com `?screen=…`** — gallery `index.html` + `screens/*.html`
4. **Status bar SVGs, Dynamic Island, home indicator** — pixel-accurate
5. **44px hit targets, safe-area insets**
6. **Por que NÃO redesenhar um celular do zero**
7. **Animações entre telas (CSS keyframes ou Framer-style)**

**Hands-on:** Brief = "app mobile de meditação — splash, onboarding (3 slides), home com cards de práticas, player de áudio". Output: 5 telas embed em iPhone frame, índice gallery.

**Fontes no repo:** `skills/mobile-app/`, `skills/mobile-onboarding/`, `apps/web/public/frames/iphone-15-pro.html`, `assets/frames/*.html`

---

### Módulo 2.4 · Carrossel Social

**Resultado de aprendizagem:** O aluno cria carrossel 1080×1080 de 3-7 cards com narrativa contínua (não cards isolados).

**Tópicos:**
1. **`social-carousel` skill — quando 1:1 vs 9:16 vs 4:5**
2. **A regra da continuidade visual** — headlines que se conectam entre cards
3. **Card 1 (hook), 2-N (proof/story), N (CTA/loop)**
4. **Loop affordance — o último card sugerindo voltar ao primeiro**
5. **Tipografia display em cards quadrados** — escala mínima, contraste
6. **Brand mark: posição, tamanho, recorrência**
7. **Export: PNG por card via Playwright (workflow imkt4 ou puppeteer)**

**Hands-on:** Brief = "carrossel de 5 cards explicando o que é OKLch para designers brasileiros". Output: 5 cards encadeados, headline contínua, brand mark.

**Fontes no repo:** `skills/social-carousel/SKILL.md`, `skills/social-carousel/assets/template.html`

---

### Módulo 2.5 · Dashboard / Tool UI

**Resultado de aprendizagem:** O aluno gera dashboard denso (KPIs + chart + tabela + sidebar) onde **densidade é feature**, não bug.

**Tópicos:**
1. **`dashboard` skill — premissa de density-first**
2. **Sidebar fixa + canvas central + right rail (opcional)**
3. **Numerais tabulares (mono digits) — por que e como**
4. **KPIs: hierarquia visual, sparklines, deltas com sinal**
5. **Tabela com tipografia tabular, hover row, sticky header**
6. **Chart: SVG inline > biblioteca pesada (escolha do agente)**
7. **Sem decoração: shadows, gradients e rounded são inimigos aqui**
8. **`dating-web` como caso editorial dentro de dashboard** — quando densidade encontra editorial

**Hands-on:** Brief = "dashboard de métricas de uma startup B2B SaaS — MRR, churn, NPS, top 10 contas". Output: index.html denso, dark mode, real-data feel.

**Fontes no repo:** `skills/dashboard/`, `skills/dating-web/` (case especial)

---

### Módulo 2.6 · Crítica & Tweaks — fechando o loop

**Resultado de aprendizagem:** O aluno usa `critique` skill para auditar artefatos próprios, e `tweaks` skill para ajustes finos guiados pelo modelo.

**Tópicos:**
1. **Quando rodar `critique` skill** — depois do primeiro draft, antes do export
2. **As 5 dimensões pontuadas 0-10** — Philosophy, Visual Hierarchy, Detail, Functionality, Innovation
3. **Output: relatório HTML com radar chart + Keep/Fix/Quick-wins**
4. **`tweaks` skill — painel de tweaks emitido pelo modelo**
5. **Quando o modelo decide o que tweakar** — sliders por hue, spacing, font-scale, opacity
6. **`POST /api/artifacts/lint` — checagem estrutural** (broken `<artifact>`, missing side-files, palette tokens velhos)
7. **Iteração: 2 passes é normal, mais que 3 é sinal de brief errado**

**Hands-on:** Pegar um artefato gerado nos módulos 2.1-2.5 e rodar `critique`. Aplicar Quick-wins. Re-pontuar.

**Fontes no repo:** `skills/critique/SKILL.md`, `skills/tweaks/SKILL.md`, `apps/daemon/src/server.ts` (`/api/artifacts/lint`)

---

## Trilha 3 — Técnicas Avançadas (purple)

> **Objetivo:** Power-user e extensibilidade. Ao final, o aluno troca providers, escreve skills próprias, integra com outros sistemas, e entende a engenharia do daemon.

### Módulo 3.1 · BYOK Proxy & Multi-modelo

**Resultado de aprendizagem:** O aluno troca o motor de design entre Claude Code, Codex, Ollama local, MiMo, DeepSeek, OpenRouter, vLLM auto-hospedado — sabendo o trade-off de cada.

**Tópicos:**
1. **`POST /api/proxy/stream` — anatomia** — `{ baseUrl, apiKey, model, messages }` → SSE pass-through
2. **Por que SSRF guard** — bloqueio de loopback / link-local / RFC1918
3. **Compatibilidade OpenAI — o padrão de fato** — `/v1/chat/completions`
4. **MiMo (Xiaomi), DeepSeek, Groq, OpenRouter — preset com `KNOWN_PROVIDERS`**
5. **Ollama local — `http://localhost:11434/v1` + qual modelo escolher** (qwen2.5-coder:32b > generalistas para HTML)
6. **Tool_choice: 'none' para MiMo — por que (schema malcomportado em geração free-form)**
7. **Quando usar BYOK proxy vs CLI agent — trade-off de skills do Claude Code**

**Hands-on:** Trocar de Claude Code para Ollama local na mesma sessão; comparar qualidade de output do mesmo brief.

**Fontes no repo:** `apps/daemon/src/server.ts` (`/api/proxy/stream`), `apps/web/src/state/config.ts` (`KNOWN_PROVIDERS`), `apps/daemon/src/agents.ts`

---

### Módulo 3.2 · Agent Client Protocol (ACP) & adapters

**Resultado de aprendizagem:** O aluno entende o ACP (JSON-RPC stdio bidirecional, "LSP para coding agents"), reconhece as 6 famílias de stream format, e adiciona um adapter novo.

**Tópicos:**
1. **O que é ACP — JSON-RPC 2.0 sobre stdio, bidirecional simétrico** ([agentclientprotocol.com](https://agentclientprotocol.com))
2. **Por que stdio (não HTTP)** — process isolation, language independence, sem porta
3. **Os 11 CLIs suportados — taxonomia por stream format** — `claude-stream-json`, `copilot-stream-json`, `json-event-stream` (Codex/Gemini/OpenCode/Cursor), `acp-json-rpc` (Hermes/Kimi/Kiro), `pi-rpc`, `plain` (Qwen)
4. **Detecção automática no boot — `PATH` scan**
5. **Por-CLI argv builders & promptViaStdin** — Windows-friendly fallbacks
6. **`AGENT_DEFS` em `apps/daemon/src/agents.ts` — anatomia**
7. **Como adicionar um novo CLI — uma entrada + um eventParser**

**Hands-on:** Adicionar um adapter "fake" (mock CLI que responde com texto fixo) ao `AGENT_DEFS` e ver aparecer no picker.

**Fontes no repo:** `apps/daemon/src/agents.ts`, `docs/agent-adapters.md` (279 linhas), `apps/daemon/src/claude-stream.ts`. Externa: [agentclientprotocol.com](https://agentclientprotocol.com), [Kiro ACP docs](https://kiro.dev/docs/cli/acp/)

---

### Módulo 3.3 · Brand-Spec Extraction Avançada

**Resultado de aprendizagem:** O aluno extrai um sistema visual de uma URL/screenshot que o cliente forneceu, sem inventar cores. Domina o protocolo de 5 passos.

**Tópicos:**
1. **O problema: agente alucinando hex codes**
2. **Os 5 passos do protocolo** — Locate · Download · grep hex · Codify · Vocalise
3. **Locate: WebFetch em `/brand`, `/press`, `/about`**
4. **Download: CSS, brand-guide PDF, screenshots — qualquer artefato**
5. **`grep -E '#[0-9a-fA-F]{3,8}'` no CSS — extração mecânica**
6. **Codify: `brand-spec.md` com 6 tokens em OKLch + 3 font stacks + 3-5 posture rules**
7. **Vocalise: declarar o sistema em uma frase** — "warm cream background, single rust accent at oklch(58% 0.15 35), Newsreader display + system body"
8. **Quando converter HEX existente para OKLch — preservar `L` perceptual**

**Hands-on:** Extrair brand-spec de uma URL (ex: stripe.com, vercel.com) usando o protocolo. Comparar com `design-systems/stripe/DESIGN.md` do repo.

**Fontes no repo:** `packages/contracts/src/prompts/discovery.ts` (Branch B), `design-systems/stripe/DESIGN.md`, `design-systems/vercel/DESIGN.md`

---

### Módulo 3.4 · Critique 5-dim como Loop — auto-crítica integrada

**Resultado de aprendizagem:** O aluno entende a crítica não como ferramenta avulsa, mas como **gate pre-emit** rodado pelo agente em todo turn.

**Tópicos:**
1. **A diferença entre `skills/critique/` (manual) e a crítica embutida no `discovery.ts`** (automática)
2. **As 5 dimensões — definição operacional precisa** — Philosophy, Hierarchy, Execution, Specificity, Restraint
3. **Score 0-10 vs. 1-5 — quando usar qual escala**
4. **O gate "anything < 3/5 é regressão"**
5. **Loop de 2 passes como norma**
6. **Integração com `POST /api/artifacts/lint`** — findings reais alimentam a próxima rodada
7. **Como aumentar/reduzir a barra por skill** — `references/checklist.md` por skill (P0 hard gate)
8. **A "anti-AI-slop blacklist" como Specificity check**

**Hands-on:** Configurar uma skill custom com critique mais agressivo (P0 inclui "no rounded cards"). Rodar e ver o agente refazer.

**Fontes no repo:** `packages/contracts/src/prompts/discovery.ts` (RULE 3, Step 8), `skills/critique/SKILL.md`, `skills/critique/references/dimensions.md`

---

### Módulo 3.5 · Criando uma Skill Própria

**Resultado de aprendizagem:** O aluno escreve uma skill end-to-end (`SKILL.md` + `assets/template.html` + `references/{layouts,checklist}.md`), instala, e o agente a usa.

**Tópicos:**
1. **Quando criar uma skill nova vs. estender uma existente**
2. **O template de pasta** — `<skill-name>/{SKILL.md, assets/, references/}`
3. **Frontmatter passo a passo** — name, description, triggers (com palavras-chave em vários idiomas), `od:` extensions
4. **`assets/template.html` — boas práticas de seed** — tokens em `:root`, comentários por seção
5. **`references/layouts.md` — por que paste-ready importa**
6. **`references/checklist.md` — escrevendo P0 que vale a pena**
7. **`example_prompt` no frontmatter — UX do picker**
8. **Onde instalar para testar — `~/.claude/skills/<nome>/`**
9. **Restart do daemon e aparição no picker**
10. **Submeter ao upstream open-design (PR pattern)**

**Hands-on:** Criar uma skill `landing-curso` específica para landings de cursos online no estilo INEMA. Tornar default para cenário "education". Testar.

**Fontes no repo:** `docs/skills-protocol.md`, `skills/web-prototype/` (template referência), `skills/dating-web/` (case complexo). Externa: [Claude Code Skills convention](https://docs.anthropic.com/en/docs/claude-code/skills)

---

### Módulo 3.6 · Daemon, Sidecar IPC & Multi-namespace

**Resultado de aprendizagem:** O aluno entende a engenharia do daemon, opera múltiplos namespaces em paralelo (Playwright + dev + projetos reais), e debuga via inspect tools.

**Tópicos:**
1. **`pnpm tools-dev` — o único entrypoint de lifecycle** — start/stop/run/status/logs/inspect/check
2. **Stamps tipados de 5 campos** — `app · mode · namespace · ipc · source`
3. **Sidecar IPC em `/tmp/open-design/ipc/<namespace>/<app>.sock`** — STATUS, EVAL, SCREENSHOT, CONSOLE, CLICK, SHUTDOWN
4. **`OD_DATA_DIR` e `--namespace` — isolamento de árvore `.od/`**
5. **Por que namespaces — Playwright, beta, projetos reais sem colisão de SQLite**
6. **`tools-dev inspect desktop screenshot` — automação E2E sem harness próprio**
7. **`apps/desktop` Electron shell — discovery de URL via IPC, sem adivinhar porta**
8. **`packages/sidecar-proto` vs `packages/sidecar` vs `packages/platform` — separação genérico/específico**
9. **Logs estruturados em `.tmp/tools-dev/<namespace>/logs/`**
10. **Debug: `pnpm tools-dev logs --namespace <name> --json`**

**Hands-on:** Rodar 2 namespaces em paralelo (`default` + `experiments`), com SQLite isolada cada um. Tirar screenshot do desktop em cada um.

**Fontes no repo:** `tools/dev/`, `apps/desktop/src/main/`, `packages/sidecar-proto/`, `packages/sidecar/`, `apps/AGENTS.md`, `tools/AGENTS.md`

---

## Estrutura por Página (formato INEMA.CLUB)

### Landing (`index.html`)
- Hero com pitch do curso (1 frase + 3 bullets)
- 3 cards de trilha (cores emerald/blue/purple), cada um clicável
- Seção "Para quem é" (designers, engineers, híbridos)
- Seção "Pré-requisitos" (curiosidade + qualquer terminal)
- Footer com link INEMA.CLUB e GitHub do open-design

### Index de cada trilha (`trilhaN/index.html`)
- Header com nome da trilha + progresso visual
- 6 cards de módulo, cada um com:
  - Título numerado (1.1, 1.2, ...)
  - Resumo em 1 linha
  - Lista expansível de tópicos (mínimo 6 por módulo)
  - Botão **"Ver Completo"** apontando para `modulo-N-N.html`
- Light mode CSS completo (obrigatório)

### Página de módulo (`modulo-N-N.html`)
- Título `text-2xl font-bold`
- Resultado de aprendizagem (callout)
- 6+ tópicos expansíveis, cada um com 3 seções:
  - **O que é** (definição clara)
  - **Por que aprender** (justificativa)
  - **Conceitos-chave** (lista bulletada)
- Bloco "Hands-on" (quando aplicável) — comando real para rodar
- Bloco "Fontes" (paths no repo + URLs externas)
- Botões `justify-start`, INEMA.CLUB link com `text-sky-400`
- Number-circle indicator nos tópicos (NUNCA setas)

---

## Verificação (como testar end-to-end)

1. **Compliance INEMA.CLUB** — rodar a skill `revisar-curso` em cada página gerada. Cada item do checklist deve passar.
2. **Open Browser Test** — abrir `curso-od/index.html` localmente:
   - Theme toggle funciona em todas as páginas
   - Cores corretas por trilha (emerald/blue/purple)
   - Light mode CSS completo (sem gradientes em fundo claro)
   - INEMA.CLUB link presente em todas
3. **Navegação** — clicar em qualquer card de trilha → ver index → clicar em qualquer módulo → ver página completa → voltar
4. **Tópicos** — todo módulo tem **mínimo 6 tópicos**, cada um com **3 seções** (O que é / Por que / Conceitos-chave)
5. **Hands-on** — comandos sugeridos rodam de fato (testar 1-2 por trilha)
6. **Fontes** — todos os paths citados existem no repo OD; todas as URLs externas resolvem

---

## Arquivos críticos do OD a referenciar (já mapeados)

| Caminho | Usado em |
|---|---|
| `packages/contracts/src/prompts/discovery.ts` (263L) | M 1.3, 1.6, 3.4 |
| `packages/contracts/src/prompts/directions.ts` (284L) | M 1.6 |
| `packages/contracts/src/prompts/system.ts` (334L) | M 1.3 |
| `packages/contracts/src/prompts/official-system.ts` (118L) | M 1.3 |
| `packages/contracts/src/prompts/deck-framework.ts` (374L) | M 2.1 |
| `apps/daemon/src/server.ts` | M 1.2, 2.6, 3.1 |
| `apps/daemon/src/agents.ts` | M 3.2 |
| `apps/daemon/src/skills.ts` | M 1.4 |
| `apps/daemon/src/claude-stream.ts` | M 3.2 |
| `apps/web/src/artifacts/parser.ts` | M 1.2 |
| `apps/web/src/state/config.ts` (`KNOWN_PROVIDERS`) | M 3.1 |
| `apps/web/src/components/SettingsDialog.tsx` | M 3.1 |
| `docs/architecture.md` (339L) | M 1.2, 3.6 |
| `docs/skills-protocol.md` (322L) | M 1.4, 3.5 |
| `docs/agent-adapters.md` (279L) | M 3.2 |
| `docs/modes.md` (273L) | M 1.4 |
| `docs/spec.md`, `docs/references.md` | M 1.1 |
| `skills/web-prototype/SKILL.md` | M 1.4, 2.2 |
| `skills/guizang-ppt/SKILL.md` + assets | M 2.1 |
| `skills/mobile-app/`, `skills/mobile-onboarding/` | M 2.3 |
| `skills/social-carousel/` | M 2.4 |
| `skills/dashboard/`, `skills/dating-web/` | M 2.5 |
| `skills/critique/`, `skills/tweaks/` | M 2.6, 3.4 |
| `tools/dev/`, `apps/desktop/src/main/` | M 3.6 |
| `packages/sidecar-proto/`, `packages/sidecar/` | M 3.6 |
| `assets/frames/*.html` | M 2.3 |

---

## Referências externas (já validadas via WebSearch)

- [Anthropic Claude Design (techcrunch, 2026-04-17)](https://techcrunch.com/2026/04/17/anthropic-launches-claude-design-a-new-product-for-creating-quick-visuals/) — M 1.1
- [Anthropic news: Introducing Claude Design](https://www.anthropic.com/news/claude-design-anthropic-labs) — M 1.1
- [github.com/alchaincyf/huashu-design](https://github.com/alchaincyf/huashu-design) — M 1.6
- [github.com/op7418/guizang-ppt-skill](https://github.com/op7418/guizang-ppt-skill) — M 2.1
- [github.com/OpenCoworkAI/open-codesign](https://github.com/OpenCoworkAI/open-codesign) — M 1.1
- [github.com/multica-ai/multica](https://github.com/multica-ai/multica) — M 1.1
- [agentclientprotocol.com](https://agentclientprotocol.com) — M 3.2
- [github.com/agentclientprotocol/agent-client-protocol](https://github.com/agentclientprotocol/agent-client-protocol) — M 3.2
- [evilmartians.com — OKLCH in CSS: why we moved from RGB and HSL](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl) — M 1.5, 3.3
- [docs.anthropic.com — Claude Code Skills](https://docs.anthropic.com/en/docs/claude-code/skills) — M 1.4, 3.5
- [github.com/farion1231/cc-switch](https://github.com/farion1231/cc-switch) — M 3.1

---

## Plano de execução (fases)

**Fase A — Esqueleto (sessão 1, ~2h)**
1. `mkdir /home/nmaldaner/projetos/curso-od/curso/{trilha1-fundamentos,trilha2-exemplos,trilha3-avancado}`
2. Carregar skill `formato-curso` e ler `MASTER_COMPLETO.md`
3. Criar `index.html` (landing) — pitch + 3 cards de trilha + footer
4. Criar 3 `trilhaN/index.html` (cards de módulo + tópicos expansíveis), respeitando cor por trilha
5. Validar com skill `revisar-curso` o esqueleto

**Fase B — Trilha 1 conteúdo (sessão 2, ~3h)**
- Escrever 6 módulos da Trilha 1, lendo material-fonte do repo OD para cada
- Cada módulo: 6+ tópicos, 3 seções por tópico, 1 hands-on quando aplicável
- Auditar com `revisar-curso`

**Fase C — Trilha 2 conteúdo (sessão 3, ~3h)**
- 6 módulos da Trilha 2 — uso prático
- Hands-on em todos (formatos diferentes)

**Fase D — Trilha 3 conteúdo (sessão 4, ~3-4h)**
- 6 módulos da Trilha 3 — avançado
- Hands-on em todos (BYOK switch, ACP adapter, brand-spec, custom skill, namespace duplo)

**Fase E — Polish (sessão 5, ~1-2h)**
- Revisar consistência cross-modules (terminologia, nomenclatura)
- Light mode em todas as páginas
- Validar links entre páginas
- Rodar `revisar-curso` final

**Esforço total estimado:** 12-15 horas distribuídas em 5 sessões.

---

## Métricas de qualidade do curso (não negociáveis)

| Métrica | Alvo |
|---|---|
| Páginas HTML criadas | 22 (1 landing + 3 trilha-index + 18 módulos) |
| Tópicos por módulo | ≥ 6 |
| Seções por tópico | exatamente 3 (O que é / Por que / Conceitos-chave) |
| Hands-on por trilha | ≥ 4 módulos com hands-on real |
| Links externos validados | 100% (já validados via WebSearch) |
| Paths no repo OD validados | 100% (já mapeados via Bash + Read) |
| Páginas sem light-mode CSS | 0 |
| Páginas sem INEMA.CLUB link | 0 |
| Botões `justify-center` (errado) | 0 — sempre `justify-start` |
| Indicadores ▶ (errado) | 0 — sempre número em círculo |
