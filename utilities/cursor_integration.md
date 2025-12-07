CURSOR INTEGRATION

The Lens Atlas integrates with Cursor through explicit **Lens** commands.

Canonical load command:

"Load lens: ./lens-atlas/lenses/{lensname}.md"

Natural-language alias (recommended when working in the Atlas):

- "Equip {LENS_NAME}"
- "Equip {LENS_NAME} lens"
- "Equip lenses: {LENS_NAME_1}, {LENS_NAME_2}"

Cursor must:

Read the Lens file.

Adopt all directives and constraints.

Merge with existing equipped Lenses via the Parent Lens.

Maintain fidelity until explicitly unequipped/unloaded.

Unload / unequip:

"Unload lens: {lensname}"

"Unequip {LENS_NAME}"

"Unequip all lenses"

Cursor then reverts to baseline (or to any remaining active Lenses).



