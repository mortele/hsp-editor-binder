### hsp-editor-binder

[![Launch Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/mortele/hsp-editor-binder/main?urlpath=lab/tree/demo.ipynb)

Open the Binder link and run `demo.ipynb`. HSP and the notebook editor are
installed during the image build; coworkers do not need a local installation.

The demo offers an empty editor with `hsp.edit_molecule()` or an ethanol editor
with `hsp.edit_molecule(hsp.Molecule('CCO'))`. Keep the returned widget in
`editor`, then run `editor.to_molecule()` after making changes to retrieve an
independent snapshot. Close an editor with its **X** button or `editor.close()`.

#### HSP source versions

The build uses Python 3.12 and the working HSP `2026-09-16` snapshot, with two
packages replaced by the paired editor MRs:

| Package | Source | Pinned commit |
| --- | --- | --- |
| hytools | [MR !273](https://gitlab.com/hylleraasplatform/hylleraas-tools/-/merge_requests/273) | `d0c2670a219d5eefc620d6638b5800cae1093acb` |
| hylleraas | [MR !88](https://gitlab.com/hylleraasplatform/hylleraas/-/merge_requests/88) | `677d147116b8d770027c8eeb07b3c0dc4033b968` |

`.binder/postBuild` installs the snapshot first, then `hytools[editor]`, then
the hylleraas wrapper with `--no-deps`. That last option preserves the snapshot
instead of following the MR's development dependencies back to `main`.
The build checks both installed commit IDs and exercises opening, building,
exporting, undoing, and closing editors before succeeding.

#### Updating the demo

After pushing changes to either MR, update `HYTOOLS_REF` or `HYLLERAAS_REF` in
`.binder/postBuild` to its full commit SHA, and update the table above. Commit
and push the Binder repository changes, then open the launch link to build the
new version. The pins do not automatically follow later MR updates.

For a link fixed to one Binder revision, replace `main` in the launch URL with
the Binder repository's commit SHA. Binder sessions are temporary; download
notebooks or exported structures you want to keep before ending a session.
