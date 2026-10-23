# Native HSA physiological pockets

Atomic structures and geometric models of eleven physiological regions in
**native, 585-residue HSA**, sampled in three independent 1 µs simulations.
The collection includes a common HSA template, individual pocket templates,
and the original R1-R3 results.

## Choose a template

The **whole-protein representative** retains all eleven binding regions in
one observed HSA conformation. It provides a common structural context for
comparing sites, examining the complete surface and modelling partners that
contact more than one part of the protein. Its atomic PDB preserves the
chemical groups; the protein hull describes the overall geometric envelope.

The **pocket-shape representatives** describe each cavity independently,
together with its lining residues and parent protein. They support local
docking preparation, cavity-shape comparisons and inspection of possible
contacts. Different pockets can come from different observed frames.

### Whole-protein representative

One observed frame is selected from the most populated group of overall HSA
conformations. **All eleven pockets are extracted from this same frame.**
Their relative positions, the shape of the protein and the surrounding residues
therefore belong to one coherent structure.

The files for this common protein conformation are in
[`whole_protein/`](structures/representative/whole_protein); the alternative
conformation is in [`whole_protein_group_2/`](structures/representative/whole_protein_group_2).

The common clustering identifies two groups. **Group 1 is the most populated
(68.3%)** and supplies the principal whole-protein template. **Group 2 (31.7%)**
is shown as an alternative conformation. Both are observed frames from the same
native HSA dataset, with the replicas contributing equally.

The guide uses the native reference cartoon and its convex hull; green
shapes illustrate the probe positions. The observed protein frames and their
calculated pocket geometries are collected below.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/whole_protein_overview_dark.svg">
  <img src="images/whole_protein_overview.svg" width="100%" alt="Schematic guide showing a whole protein, pocket probes, their overlay and the protein convex hull">
</picture>

<details>
<summary>Whole HSA - view all representations</summary>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/HSA_common_representative_dark.png">
  <img src="images/HSA_common_representative.png" width="100%" alt="The two common native HSA conformations in the same frontal view, with physiological probes and the group 1 protein envelope">
</picture>

The two frontal views use the same Domain II alignment, camera and molecular
scale. The cartoon shows HSA secondary structure; saturated colors identify the
pocket probe spaces. For each group, all eleven pocket geometries were computed
from the same whole-protein frame.
The separate wireframe shows the complete protein convex hull of group 1. A convex hull bridges surface indentations;
it is a coarse geometric envelope. The atomic PDB retains atomic detail and chemical identities.

- [Group 1 protein PDB](structures/representative/whole_protein/protein.pdb)
- [Group 2 protein PDB](structures/representative/whole_protein_group_2/protein.pdb)
- [Group 2 protein and pockets](structures/representative/whole_protein_group_2/HSA_with_all_pockets.pdb)
- [Protein with all probes, PDB](structures/representative/whole_protein/HSA_with_all_pockets.pdb)
- [Protein hull with all probes, PDB](structures/representative/whole_protein/HSA_hull_with_all_pockets.pdb)
- [Protein hull with all probes, OBJ](structures/representative/whole_protein/HSA_hull_with_all_pockets.obj)
- [Protein hull with all probes, SDF](structures/representative/whole_protein/HSA_hull_with_all_pockets.sdf)
- [Complete group 2 models](structures/representative/whole_protein_group_2)

#### Group 1 · dominant conformation

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/HSA_group_1_representations_dark.png">
  <img src="images/HSA_group_1_representations.png" width="100%" alt="Group 1 observed HSA frame in four matching views: structure, all probes, structure with probes and the complete protein hull with probes">
</picture>

#### Group 2 · alternative conformation

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/HSA_group_2_representations_dark.png">
  <img src="images/HSA_group_2_representations.png" width="100%" alt="Group 2 observed HSA frame in four matching views: structure, all probes, structure with probes and the complete protein hull with probes">
</picture>

All four panels for each group use the same observed parent frame, camera and
molecular scale. Protein-only views use an opaque NewCartoon; overlays use
the transparent cartoon to show the probe positions. Probe-only views retain
their positions within the complete protein. The envelope is the convex hull
stored in `protein_hull.*`.

</details>

### Pocket-shape representatives

Each pocket is considered separately. Frames containing space for the probe
are compared across the three simulations, and one observed frame is selected
to represent the most populated group of nonempty cavity shapes. The selection
reflects the **shape of that pocket**, including where its internal space lies.

These models retain each selected cavity and its lining residues.
Different pockets can come from different frames. Each model includes its own
complete parent protein and geometric envelope. The selected structures are
observed conformations; the trajectory averages are reported separately below.
The files are in [`pocket_geometry/`](structures/representative/pocket_geometry).

The schematic example introduces four views: **atomic pocket residues**,
**probe surface**, **residues with the probe**, and **residue convex hull**.
Green shows the internal probe space; the amber wireframe encloses the lining
atoms.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/representations_overview_dark.svg">
  <img src="images/representations_overview.svg" width="100%" alt="Schematic pocket example showing atomic residues, probe space, their overlay and the residue convex hull">
</picture>

Expand a pocket below to see its measured structures. The rows show the common
whole-protein frame, the pocket-shape frame and an observed frame with volume
closest to the trajectory mean. All twelve panels for each pocket share the
same local alignment and molecular scale.
The probe mesh stored in `probe.obj` and `probe.ply` retains the 1 Å grid used
for the calculation. The lining-atom envelope is stored in `lining_hull.*`.

<details>
<summary>Sudlow I - view all representations</summary>

#### Sudlow I

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/Sudlow_I_representatives_dark.png">
  <img src="images/Sudlow_I_representatives.png" width="100%" alt="Sudlow I: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/Sudlow_I/`](structures/representative/whole_protein/Sudlow_I) ·
[`pocket_geometry/Sudlow_I/`](structures/representative/pocket_geometry/Sudlow_I) ·
[`mean_volume/Sudlow_I/`](structures/representative/mean_volume/Sudlow_I)

</details>

<details>
<summary>Sudlow II - view all representations</summary>

#### Sudlow II

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/Sudlow_II_representatives_dark.png">
  <img src="images/Sudlow_II_representatives.png" width="100%" alt="Sudlow II: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/Sudlow_II/`](structures/representative/whole_protein/Sudlow_II) ·
[`pocket_geometry/Sudlow_II/`](structures/representative/pocket_geometry/Sudlow_II) ·
[`mean_volume/Sudlow_II/`](structures/representative/mean_volume/Sudlow_II)

</details>

<details>
<summary>Heme - view all representations</summary>

#### Heme

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/Heme_representatives_dark.png">
  <img src="images/Heme_representatives.png" width="100%" alt="Heme: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/Heme/`](structures/representative/whole_protein/Heme) ·
[`pocket_geometry/Heme/`](structures/representative/pocket_geometry/Heme) ·
[`mean_volume/Heme/`](structures/representative/mean_volume/Heme)

</details>

<details>
<summary>Cleft - view all representations</summary>

#### Cleft

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/Cleft_representatives_dark.png">
  <img src="images/Cleft_representatives.png" width="100%" alt="Cleft: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/Cleft/`](structures/representative/whole_protein/Cleft) ·
[`pocket_geometry/Cleft/`](structures/representative/pocket_geometry/Cleft) ·
[`mean_volume/Cleft/`](structures/representative/mean_volume/Cleft)

</details>

<details>
<summary>FA1 - view all representations</summary>

#### FA1

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/FA1_representatives_dark.png">
  <img src="images/FA1_representatives.png" width="100%" alt="FA1: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/FA1/`](structures/representative/whole_protein/FA1) ·
[`pocket_geometry/FA1/`](structures/representative/pocket_geometry/FA1) ·
[`mean_volume/FA1/`](structures/representative/mean_volume/FA1)

</details>

<details>
<summary>FA2 - view all representations</summary>

#### FA2

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/FA2_representatives_dark.png">
  <img src="images/FA2_representatives.png" width="100%" alt="FA2: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/FA2/`](structures/representative/whole_protein/FA2) ·
[`pocket_geometry/FA2/`](structures/representative/pocket_geometry/FA2) ·
[`mean_volume/FA2/`](structures/representative/mean_volume/FA2)

</details>

<details>
<summary>FA3 - view all representations</summary>

#### FA3

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/FA3_representatives_dark.png">
  <img src="images/FA3_representatives.png" width="100%" alt="FA3: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/FA3/`](structures/representative/whole_protein/FA3) ·
[`pocket_geometry/FA3/`](structures/representative/pocket_geometry/FA3) ·
[`mean_volume/FA3/`](structures/representative/mean_volume/FA3)

</details>

<details>
<summary>FA4 - view all representations</summary>

#### FA4

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/FA4_representatives_dark.png">
  <img src="images/FA4_representatives.png" width="100%" alt="FA4: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/FA4/`](structures/representative/whole_protein/FA4) ·
[`pocket_geometry/FA4/`](structures/representative/pocket_geometry/FA4) ·
[`mean_volume/FA4/`](structures/representative/mean_volume/FA4)

</details>

<details>
<summary>FA5 - view all representations</summary>

#### FA5

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/FA5_representatives_dark.png">
  <img src="images/FA5_representatives.png" width="100%" alt="FA5: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/FA5/`](structures/representative/whole_protein/FA5) ·
[`pocket_geometry/FA5/`](structures/representative/pocket_geometry/FA5) ·
[`mean_volume/FA5/`](structures/representative/mean_volume/FA5)

</details>

<details>
<summary>FA6 - view all representations</summary>

#### FA6

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/FA6_representatives_dark.png">
  <img src="images/FA6_representatives.png" width="100%" alt="FA6: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/FA6/`](structures/representative/whole_protein/FA6) ·
[`pocket_geometry/FA6/`](structures/representative/pocket_geometry/FA6) ·
[`mean_volume/FA6/`](structures/representative/mean_volume/FA6)

</details>

<details>
<summary>FA7 - view all representations</summary>

#### FA7

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/FA7_representatives_dark.png">
  <img src="images/FA7_representatives.png" width="100%" alt="FA7: atomic residues, probe mesh, residues with probe and convex hull, compared across whole-protein, pocket-shape and near-mean-volume frames">
</picture>

[`whole_protein/FA7/`](structures/representative/whole_protein/FA7) ·
[`pocket_geometry/FA7/`](structures/representative/pocket_geometry/FA7) ·
[`mean_volume/FA7/`](structures/representative/mean_volume/FA7)

</details>

## Pocket volumes

**MD mean ± SD** reports the average of the three replica means and their
between-replica SD. Each replica mean includes all 102 sampled observations,
including frames with zero accessible probe space.

**Group 1** and **Group 2** give the volumes in the two whole-protein frames.
**Pocket shape** gives the volume in the frame selected by cavity geometry.
These selection criteria describe protein opening or local shape, so their
volumes can differ from the ensemble mean.

**Near mean** gives an additional observed frame whose volume is closest to
the MD mean among the 306 sampled frames. The models are in
[`mean_volume/`](structures/representative/mean_volume). They provide a
reference for the average cavity size, using real coordinates. All volumes
are in Å³. Click a value to open its model folder.

| Pocket | MD mean ± SD | Group 1 | Group 2 | Pocket shape | Near mean |
|---|---:|---:|---:|---:|---:|
| Sudlow&nbsp;I | 65.9 ± 13.4 | [50](structures/representative/whole_protein/Sudlow_I) | [55](structures/representative/whole_protein_group_2/Sudlow_I) | [114](structures/representative/pocket_geometry/Sudlow_I) | [66](structures/representative/mean_volume/Sudlow_I) |
| Sudlow&nbsp;II | 16.4 ± 10.6 | [24](structures/representative/whole_protein/Sudlow_II) | [3](structures/representative/whole_protein_group_2/Sudlow_II) | [36](structures/representative/pocket_geometry/Sudlow_II) | [16](structures/representative/mean_volume/Sudlow_II) |
| Heme | 173.5 ± 36.9 | [136](structures/representative/whole_protein/Heme) | [63](structures/representative/whole_protein_group_2/Heme) | [383](structures/representative/pocket_geometry/Heme) | [174](structures/representative/mean_volume/Heme) |
| Cleft | 233.5 ± 103.8 | [250](structures/representative/whole_protein/Cleft) | [392](structures/representative/whole_protein_group_2/Cleft) | [307](structures/representative/pocket_geometry/Cleft) | [231](structures/representative/mean_volume/Cleft) |
| FA1 | 41.0 ± 13.1 | [0](structures/representative/whole_protein/FA1) | [60](structures/representative/whole_protein_group_2/FA1) | [129](structures/representative/pocket_geometry/FA1) | [41](structures/representative/mean_volume/FA1) |
| FA2 | 5.7 ± 4.6 | [1](structures/representative/whole_protein/FA2) | [0](structures/representative/whole_protein_group_2/FA2) | [11](structures/representative/pocket_geometry/FA2) | [6](structures/representative/mean_volume/FA2) |
| FA3 | 4.2 ± 4.4 | [0](structures/representative/whole_protein/FA3) | [3](structures/representative/whole_protein_group_2/FA3) | [3](structures/representative/pocket_geometry/FA3) | [4](structures/representative/mean_volume/FA3) |
| FA4 | 57.9 ± 33.2 | [53](structures/representative/whole_protein/FA4) | [36](structures/representative/whole_protein_group_2/FA4) | [120](structures/representative/pocket_geometry/FA4) | [58](structures/representative/mean_volume/FA4) |
| FA5 | 14.1 ± 15.0 | [26](structures/representative/whole_protein/FA5) | [1](structures/representative/whole_protein_group_2/FA5) | [38](structures/representative/pocket_geometry/FA5) | [14](structures/representative/mean_volume/FA5) |
| FA6 | 169.1 ± 24.5 | [168](structures/representative/whole_protein/FA6) | [181](structures/representative/whole_protein_group_2/FA6) | [199](structures/representative/pocket_geometry/FA6) | [169](structures/representative/mean_volume/FA6) |
| FA7 | 9.3 ± 5.5 | [2](structures/representative/whole_protein/FA7) | [0](structures/representative/whole_protein_group_2/FA7) | [25](structures/representative/pocket_geometry/FA7) | [9](structures/representative/mean_volume/FA7) |

A zero means that the 1.4 Å probe has no accessible center positions within
the specified region in that frame. The physiological site is still defined by
its reference residues. These volumes describe the selected probe and region;
FA7 overlaps Sudlow I, and FA3/FA4 overlap Sudlow II.

[Full comparison table](tables/representative_comparison.csv) ·
[Source frames and lining residues](tables/representative_models.csv) ·
[Near-mean-volume frames](tables/mean_volume_models.csv) ·
[Methods and table definitions](tables/README.md)

## Find the files

```text
structures/
├── representative/
│   ├── whole_protein/          Group 1: principal HSA template
│   ├── whole_protein_group_2/  Group 2: alternative HSA conformation
│   ├── pocket_geometry/        One shape-selected frame for each pocket
│   └── mean_volume/            One frame closest to each mean pocket volume
├── R1/                     Original per-replica models
├── R2/
└── R3/
tables/                     Volumes, source frames and methods
images/                     Transparent previews
```

Pocket models are stored under `structures/representative/` in
`whole_protein/<site>/`, `whole_protein_group_2/<site>/`,
`pocket_geometry/<site>/` and `mean_volume/<site>/`. For example, the
shape-selected FA1 model is in
[`pocket_geometry/FA1/`](structures/representative/pocket_geometry/FA1), and
the near-mean FA1 model is in
[`mean_volume/FA1/`](structures/representative/mean_volume/FA1).
These directories contain the models listed below. Coordinates are in Å.

| File | Contents |
|---|---|
| `pocket_atoms.pdb` | Residues with heavy atoms within 4 Å of the probe mesh in this frame |
| `region_atoms.pdb` | Alignment-anchor residues used to place the reference pocket region on this frame |
| `probe.pdb`, `.obj`, `.ply` | Accessible probe-center space |
| `lining_hull.pdb`, `.obj`, `.ply` | Convex envelope of the lining-residue heavy atoms |
| `pocket_with_geometry.pdb` | Pocket atoms, probe model and complete protein hull |
| `protein_with_pocket.pdb` | Complete protein, that pocket's probe and protein hull |
| `protein.pdb`, `protein_hull.*` | Complete parent protein and its hull; inside `pocket_geometry/<site>/` and `mean_volume/<site>/`, or in the parent `whole_protein/` and `whole_protein_group_2/` directories |

`probe.obj`, `lining_hull.obj` and `protein_hull.obj` also have matching
**SDF, MOL and MOL2** exports. Their vertices and edges describe geometry.
They use virtual atoms (`*` or `Du`); chemical atoms remain in the atomic
PDB files. OBJ/PLY retain the triangular surface faces.

The original R1, R2 and R3 models and numerical results are retained. Each replica
has two whole-protein cluster representatives, with all eleven regions extracted
from each frame. Frame identities, clustering details and the definitions of all
tables are in [Methods and numerical results](tables/README.md).

## License

The original structures, geometric models, numerical tables, figures and
documentation in this collection are licensed under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE).

Reuse and adaptation, including commercial use, are permitted with appropriate
credit, a link to the license and an indication of any changes. Please identify
this collection and retain the author and source information supplied with
the material.

Third-party material retains its original terms and attribution.
