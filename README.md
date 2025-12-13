# Lens Atlas

**Modular cognitive engines for AI agents.**

---

## The Premise

AI behavior is usually invisible—buried in system prompts, scattered across conversations, impossible to version or share.

Lens Atlas makes it explicit. Each **Lens** is a self-contained specification that defines how an AI thinks: its purpose, identity, methods, guardrails, and activation protocol. Load a lens, and the agent transforms. Unload it, and it reverts.

No magic. Just structured text files that agents read and follow.

---

## What Lenses Are

A Lens is a cognitive engine encoded in Markdown. It defines:

- **Purpose**: What the lens exists to do
- **Identity & Role**: Persona, tone, epistemic stance
- **Scope of Competence**: What it does and doesn't do
- **Core Methods**: How it thinks and acts
- **Guardrails**: Safety rules, hallucination prevention, scope enforcement
- **Activation Protocol**: What changes when loaded

Think of lenses as portable personalities with procedures. Unlike one-off prompts, they're:

- **Modular**: Use one lens, or stack several
- **Reusable**: Apply the same lens across projects
- **Versionable**: Track changes in Git like code
- **Shareable**: Build a library, trade with others

---

## Philosophy

### Explicit Over Implicit

Most AI behavior is a black box. Lens Atlas brings it into the open. Every capability, constraint, and procedure is written down, readable, and editable.

### Composable Reasoning

Complex tasks need different thinking modes. A planning lens decomposes the problem. A writing lens drafts the output. A critic lens reviews it. Stack them, swap them, evolve them.

### Files Are the Interface

No special tooling required. Lenses are Markdown files. Load them by referencing the path. The file system is the API.

### Safety by Design

Every lens includes explicit guardrails—what it won't do, how it handles ambiguity, how it prevents hallucination. Safety isn't an afterthought; it's built into the specification.

---

## How It Works

### Load a Lens

In Cursor (or any compatible LLM interface):

```
Load lens: ./lenses/example_lens.md
```

Or use natural language:

```
Equip MANA
Equip Signal Architect lens
Equip lenses: Lyra, TherapyNotes Forge
```

### What Happens

1. Agent reads the lens file
2. Adopts its identity, methods, and constraints
3. Obeys global safety rules in `core/global_safety.md`
4. Maintains fidelity until unloaded

### Unload

```
Unload lens: MANA
Unequip all lenses
```

Agent reverts to baseline behavior.

---

## Structure

```
lens-atlas/
├── README.md                 # You are here
├── lens_index.md             # Browse all public lenses
├── core/                     # Global standards and protocols
│   ├── lens_specification.md # The canonical lens template
│   ├── global_safety.md      # Safety rules for all lenses
│   ├── atlas_protocol.md     # How the system works
│   └── operational_principles.md
├── lenses/                   # Individual lens definitions
│   ├── example_lens.md       # Educational example with comments
│   ├── mana.md
│   ├── signal_architect.md
│   └── ...
└── utilities/                # Integration guides
    ├── combinator.md         # Stacking multiple lenses
    ├── parent_lens.md        # Hierarchy and conflict resolution
    └── troubleshooting.md
```

---

## Quick Start

### 1. Clone or copy

```bash
git clone https://github.com/shamanakin/lens-atlas.git
```

### 2. Browse available lenses

Open `lens_index.md` to see all public lenses with descriptions.

### 3. Load your first lens

```
Load lens: ./lenses/example_lens.md
```

This loads an educational example (TASK_DECOMPOSER) with comments explaining each section.

### 4. Build your own

1. Copy `lenses/example_lens.md`
2. Follow the structure in `core/lens_specification.md`
3. Fill in purpose, identity, scope, methods, guardrails
4. Save and load

---

## Featured Lenses

| Lens | What It Does |
|------|--------------|
| **MANA** | High-cognition transmission with maximal signal density |
| **Signal Architect** | Design custom GPT instructions with precision |
| **Lyra** | Optimize prompts for better AI performance |
| **TherapyNotes Forge** | Transform session notes into clinical documentation |
| **Suno Prompt Crafter** | Generate production-ready music prompts |
| **Super Self-Helper** | Interactive journaling with therapeutic structure |

See `lens_index.md` for the complete list.

---

## Extracting Lenses from CustomGPTs

If you already use CustomGPTs, you can convert them to lenses:

1. Analyze the CustomGPT configuration (instructions, capabilities, limitations)
2. Map its behavior into the Lens Specification Template
3. Save as a new lens file
4. Validate purpose, scope, and guardrails are clear

This turns one-off configurations into reusable, versionable, stackable lenses.

---

## Stacking Lenses

You can equip multiple lenses simultaneously:

```
Equip lenses: Signal Architect, MANA
```

Conflict resolution rules live in:
- `core/global_safety.md`
- `utilities/combinator.md`
- `utilities/parent_lens.md`

General principle: more specific lenses override more general ones, but global safety rules always win.

---

## Origins

Lens Atlas is part of the BEOS (BrightEyed Operating System) ecosystem of AI-assisted productivity tools, alongside:

- **InfoHunter**: Research and discovery
- **InkWell**: Long-form writing with voice preservation

It inherits the core philosophy: files are memory, English is code, transparency over magic.

---

## License

MIT. Use it, fork it, build your own atlas.

---

*Lens Atlas makes AI behavior explicit, modular, and evolvable. Load a lens, transform the agent, version the change.*
