# Lens Atlas

![Lens Atlas System](assets/lens-atlas-infographic.png)

The **Lens Atlas** is a file-based system for defining modular cognitive engines called **Lenses** (a coined term for this architecture) that can be loaded into any Cursor session. Each Lens is a self-contained specification describing purpose, identity, scope, methods, and guardrails, allowing you to switch or combine reasoning modes in a controlled way.

## What Lenses Are and Why They Exist

Lenses exist to make AI behavior **explicit, modular, and reusable**. Instead of burying logic in ad-hoc prompts, each Lens encodes a focused capability (e.g., planner, reviewer, researcher) with clear boundaries and safety constraints. This makes complex workflows easier to share, debug, and evolve.

## How This Relates to CustomGPTs

If you already build and use CustomGPTs, the Lens Atlas is essentially a way to:

- **Embed that functionality directly into Cursor** using plain files, not a separate UI.
- **Version, diff, and refactor** your “GPT logic” alongside code in Git.
- **Stack and hot-swap** behaviors (e.g., planner + critic + note-compressor) instead of being locked into one CustomGPT at a time.

Conceptually:

- A **CustomGPT** is a hosted configuration with instructions, tools, and memory bound to a single endpoint.
- A **Lens** is that same idea, but expressed as a text file in your repo:
  - lives next to your code and docs
  - is editable in any editor
  - can be loaded into any Cursor session via `Load lens: ./path/to/lens.md`.

If you’ve ever wanted to:

- reuse the same “persona” or reasoning style across multiple projects,
- keep a **library of workflows** (planners, reviewers, briefers, generators) under version control,
- or **mix and match** what a GPT can do on the fly inside your dev environment,

then the Lens Atlas gives you a simple, file-based way to do that without replacing your existing CustomGPTs. You can keep using CustomGPTs for hosted experiences while turning the best of those configs into Lenses for day-to-day work inside Cursor.

## Project Structure

- `core/` – Global standards, safety rules, and operational principles for all Lenses.
- `lenses/` – Individual Lens definitions (one Lens per file, using the Lens Specification Template). You can optionally maintain:
  - public Lenses (intended for sharing)
  - personal or brand-internal Lenses (kept private via `.gitignore` rules or a `lenses/private/` folder).
- `utilities/` – Integration guides and meta-Lenses (e.g., Parent Lens, combinator behavior, troubleshooting).

See `lens_index.md` for an overview of all current Lenses and suggested visibility (public vs. personal/internal).

## Getting Started in Cursor

The Lens Atlas is designed to sit **next to** whatever project you are actively working on in Cursor.

1. **Copy or clone** this folder into the root of a workspace you open in Cursor, for example:  
   - `./GIT/lens-atlas/` (as in this repository), or  
   - `./lens-atlas/` in the root of your project.
2. Open your project in Cursor as usual; the Atlas files simply need to exist somewhere in the workspace tree.
3. In any chat with Cursor, you can now **equip Lenses by file path or by name** (see below).

## How to Load or Equip Lenses in Cursor

When working in Cursor with the Lens Atlas open, you can control behavior using Lens commands.

Canonical file-path command:

- **Load a Lens**:  
  `Load lens: ./GIT/lens-atlas/lenses/example_lens.md`

Natural-language aliases:

- **Equip a Lens** (alias for load):  
  `Equip EXAMPLE_LENS`  
  `Equip Coherence Builder lens`  
  `Equip lenses: EXAMPLE_LENS, MANA`

Once equipped/loaded, Cursor should:

1. Read the Lens file.
2. Adopt its identity, procedures, and constraints.
3. Obey global safety rules in `core/global_safety.md`.
4. Maintain fidelity to the active Lenses until they are unequipped or replaced.

To **unload / unequip** a Lens:

- `Unload lens: EXAMPLE_LENS`  
- `Unequip EXAMPLE_LENS`  
- `Unequip all lenses`

Cursor should then revert to baseline behavior (or to the remaining active Lenses, if any).

You can freely **stack** multiple Lenses; conflict resolution rules live in:

- `core/global_safety.md`
- `core/atlas_protocol.md`
- `utilities/combinator.md`
- `utilities/parent_lens.md`

For most users, it is enough to think in terms of:

- **Equip one or more Lenses** for the current task.
- **Unequip** them when you want to go back to a neutral, non-lensed mode.

## Building Your Own Lens (Quick Guide)

The easiest path is:

1. **Copy `example_lens.md`** from `lenses/` and rename it, e.g. `my_new_lens.md`.
2. Open `core/lens_specification.md` and use it as the canonical checklist for required sections.
3. Fill in:
   - **Purpose** – what this Lens is for (and not for).
   - **Identity & Role** – persona, tone, epistemic stance.
   - **Scope of Competence** – explicit DO / DO NOT.
   - **Core Methods & Procedures** – how the Lens thinks and acts.
   - **Guardrails** – safety, hallucination prevention, ambiguity rules.
   - **Activation Protocol** – what changes when the Lens is equipped.
   - **Meta-Directives** – strictness, initiative, conflict rules.
4. Save it under `lenses/` (or `lenses/private/` if it is personal) and then:
   - `Load lens: ./path/to/your/lens.md`
   - or: `Equip MY_NEW_LENS`

You can also **extract a Lens from an existing system prompt or CustomGPT**:

## Extracting a Lens from a CustomGPT

To convert a CustomGPT into a Lens:

1. Analyze the CustomGPT configuration (instructions, capabilities, limitations).
2. Map its behavior into the **Lens Specification Template** in `core/lens_specification.md`.
3. Save it as a new Lens file in `lenses/`, e.g. `research_lens.md`.
4. Validate that:
   - Purpose, scope, and guardrails are clearly stated.
   - Methods and activation behavior are unambiguous.
   - Global safety rules are compatible and not violated.

This turns a one-off configuration into a reusable Lens compatible with the Lens Atlas.

## Basic Usage Examples

- **Single-Lens session**
  - `Load lens: ./GIT/lens-atlas/lenses/example_lens.md`  
  - Then: "Using the active lens, plan my project to launch a simple landing page in four weeks."

- **Swapping Lenses mid-session**
  - `Unload lens: EXAMPLE_LENS`  
  - `Load lens: ./GIT/lens-atlas/lenses/{other_lens}.md`

- **From scratch with a new Lens**
  - Create `./GIT/lens-atlas/lenses/my_new_lens.md` using the template.  
  - `Load lens: ./GIT/lens-atlas/lenses/my_new_lens.md`  
  - Interact according to the defined identity, scope, and guardrails.

Keep each Lens focused, well-scoped, and compliant with the global safety rules so the Atlas remains predictable and safe as it grows.



