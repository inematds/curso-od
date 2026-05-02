# Curso Open Design — STATUS

> **Para o próximo Claude que abrir este projeto:** leia este arquivo + `PLANO.md` e continue de onde parou. Tudo o que precisa está aqui.

## Resumo em uma linha

Curso de 3 trilhas sobre Open Design no formato INEMA.CLUB. **4 de 22 páginas HTML prontas (18%).** Falta escrever os 18 módulos.

## Estado atual (2026-05-02)

```
curso-od/
├── PLANO.md                                    ✅ 32KB · plano completo aprovado
├── STATUS.md                                   ✅ este arquivo
├── index.html                                  ✅ 20KB · landing do curso
└── curso/
    ├── trilha1-fundamentos/index.html          ✅ 68KB · 6 cards + 42 tópicos expansíveis
    ├── trilha2-exemplos/index.html             ✅ 68KB · 6 cards + 43 tópicos expansíveis
    ├── trilha3-avancado/index.html             ✅ 76KB · 6 cards + 49 tópicos expansíveis
    │
    ├── trilha1-fundamentos/modulo-1-1.html     ❌ FALTANDO — Por que Open Design existe
    ├── trilha1-fundamentos/modulo-1-2.html     ❌ FALTANDO — Arquitetura mental
    ├── trilha1-fundamentos/modulo-1-3.html     ❌ FALTANDO — Stack de Prompts é o Produto
    ├── trilha1-fundamentos/modulo-1-4.html     ❌ FALTANDO — Skills (SKILL.md)
    ├── trilha1-fundamentos/modulo-1-5.html     ❌ FALTANDO — Design Systems (DESIGN.md)
    ├── trilha1-fundamentos/modulo-1-6.html     ❌ FALTANDO — Junior-Designer Mode
    │
    ├── trilha2-exemplos/modulo-2-1.html        ❌ FALTANDO — Pitch Deck (guizang-ppt)
    ├── trilha2-exemplos/modulo-2-2.html        ❌ FALTANDO — Landing Page SaaS
    ├── trilha2-exemplos/modulo-2-3.html        ❌ FALTANDO — App Mobile Multi-tela
    ├── trilha2-exemplos/modulo-2-4.html        ❌ FALTANDO — Carrossel Social
    ├── trilha2-exemplos/modulo-2-5.html        ❌ FALTANDO — Dashboard / Tool UI
    ├── trilha2-exemplos/modulo-2-6.html        ❌ FALTANDO — Crítica & Tweaks
    │
    ├── trilha3-avancado/modulo-3-1.html        ❌ FALTANDO — BYOK Proxy & Multi-modelo
    ├── trilha3-avancado/modulo-3-2.html        ❌ FALTANDO — ACP & adapters
    ├── trilha3-avancado/modulo-3-3.html        ❌ FALTANDO — Brand-Spec Extraction
    ├── trilha3-avancado/modulo-3-4.html        ❌ FALTANDO — Critique 5-dim como Loop
    ├── trilha3-avancado/modulo-3-5.html        ❌ FALTANDO — Criando uma Skill Própria
    └── trilha3-avancado/modulo-3-6.html        ❌ FALTANDO — Daemon, Sidecar IPC
```

## Decisões fechadas

- **Local:** `/home/nmaldaner/projetos/curso-od/`
- **Audiência:** híbrida (designer-engineer)
- **Tamanho:** 6 módulos por trilha = 18 módulos
- **Mínimo 6 tópicos por módulo**, 3 seções por tópico (O que é / Por que aprender / Conceitos-chave)
- **Idioma:** Português (BR)
- **Formato:** INEMA.CLUB — skill `formato-curso` em `~/.claude/skills/formato-curso/`
- **Cores por trilha:** T1 emerald · T2 blue · T3 purple

## Recursos pra continuar

| Recurso | Caminho |
|---|---|
| Plano completo (todas as decisões) | `./PLANO.md` |
| Template/regras INEMA.CLUB | `~/.claude/skills/formato-curso/SKILL.md` |
| Templates HTML (Sec. 5/7/8/9/10) | `~/.claude/skills/formato-curso/references/MASTER_COMPLETO.md` |
| Checklist de validação | `~/.claude/skills/formato-curso/references/CHECKLIST_REVISAO.md` |
| Repo do Open Design (fontes do conteúdo) | `/home/nmaldaner/projetos/open-design/` |
| Página exemplo de índice (use como base) | `./curso/trilha1-fundamentos/index.html` |

## Conteúdo dos 18 módulos

Está detalhado no `PLANO.md` — cada módulo tem:
- **Resultado de aprendizagem** (uma frase)
- **Lista de tópicos** (mín 6)
- **Hands-on** quando aplicável
- **Fontes no repo OD** (paths para `Read`)

Procurar por "Trilha 1 — Fundamentos", "Trilha 2 — Exemplos de Uso", "Trilha 3 — Técnicas Avançadas" no `PLANO.md`.

## Estrutura de cada página de módulo (Sec. 6.2 MASTER)

```
- Navigation global (mesmo do índice da trilha, com link da trilha ativa)
- Breadcrumb (Início / Trilha X / Módulo X.X)
- Header com gradient da cor da trilha (badge MÓDULO X.X + título + stats)
- 6 Sections de tópico (número grande w-12 h-12 em círculo + h2 + intro + boxes)
   - Boxes variados: Conceito Principal / Dados / Dica Prática / Fazer-vs-Evitar / Timeline
- Bloco "Hands-on" (comando real para rodar)
- Bloco "Fontes" (paths repo + URLs externas)
- Resumo do Módulo (Sec 7.14 do MASTER)
- Footer
```

## Regras críticas (NUNCA quebrar)

- Botões SEMPRE `justify-start`
- Tópicos com **número em círculo**, NUNCA setas
- Cada tópico = 3 seções: O que é / Por que aprender / Conceitos-chave
- Link `INEMA.CLUB` em TODAS as páginas com `text-sky-400`
- **Mínimo 6 tópicos por módulo**
- Light mode CSS completo
- Título do módulo `text-2xl font-bold`
- Cor por trilha: T1 emerald (#059669 light), T2 blue (#2563eb light), T3 purple (#7c3aed light)

## Próximo passo concreto

Ao retomar, abrir Claude/Codex em `/home/nmaldaner/projetos/curso-od/` e dizer:
> "Lê STATUS.md e PLANO.md. Continua escrevendo os módulos de onde parou."

O agente saberá exatamente o que fazer.

## Tentativas anteriores que falharam

Lançar 3 agentes em paralelo (1 por trilha) com prompts grandes pedindo pra ler MASTER + repo OD antes de escrever — **3 timeouts sem escrever nada**. Ficaram presos lendo durante os 18min de timeout.

**Lição:** prompts pra agentes devem ser focados em UM módulo por vez, com o template inline (já recortado do MASTER), e instrução de escrever IMEDIATAMENTE. Ler menos, escrever mais.
