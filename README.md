# Native HSA physiological pockets

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/banner_dark.svg">
  <img src="images/banner.svg" width="100%" alt="Native HSA and three views of its heme pocket: lining residues, internal probe space and geometric envelope">
</picture>

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

The **mean-volume models** add one observed frame per pocket with cavity
volume closest to the trajectory mean. This selection describes typical size;
the pocket-shape selection describes the spatial distribution of cavity space.

| Model | How the frame is chosen | Structural context |
|---|---|---|
| Whole protein | Closest observed frame to the center of a protein-opening group | All eleven pockets belong to one HSA frame |
| Pocket shape | Most central cavity shape in the dominant nonempty shape group | Each pocket has its own source frame and complete protein |
| Mean volume | Observed volume closest to the sampled mean | Each pocket has its own source frame and complete protein |

### How the protein groups were selected

The comparison uses Domain I-III distance, the I-II-III opening angle and the
fraction of native I-III contacts. These three measurements are standardized
and compared on 600 equally sampled frames, 200 from each replica.

**Ward** starts with individual frames and successively joins the groups that
produce the smallest increase in their internal variation. **DBSCAN** identifies
dense regions using a neighborhood radius and minimum neighbor count; sparse
frames can remain unassigned. K-means groups frames around fitted centers.

| Method | Groups | Assigned training frames | Silhouette | Coverage × silhouette |
|---|---:|---:|---:|---:|
| Ward | 2 | 100.0% | 0.382 | 0.382 |
| K-means | 2 | 100.0% | 0.366 | 0.366 |
| DBSCAN | 3 | 68.2% | 0.293 | 0.200 |

Ward gives the highest score among the tested candidates and supplies the
whole-protein templates. The best eligible DBSCAN candidate leaves 31.8% of
the training sample unassigned. Applying that density model to all saved frames
leaves 33.0% unassigned. The supplied Ward groups cover all frames and provide
two representative opening geometries. Their populations refer to this
classification of the sampled trajectories.

Pocket-shape clustering is a separate calculation: it compares locally aligned
cavity masks. DBSCAN was selected for FA5; the other pockets were summarized by
one nonempty shape group. Choosing a mean-volume frame involves no clustering.
[Methods and complete comparisons](tables/README.md).

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
- [Group 2 protein and pockets](structures/representative/whole_protein_group_2/protein_with_probes_and_hull.pdb)
- [Protein with all probes, PDB](structures/representative/whole_protein/protein_with_probes_and_hull.pdb)
- [Protein hull with all probes, PDB](structures/representative/whole_protein/probes_protein_hull.pdb)
- [Protein hull with all probes, OBJ](structures/representative/whole_protein/probes_protein_hull.obj)
- [Protein hull with all probes, SDF](structures/representative/whole_protein/probes_protein_hull.sdf)
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

#### Protein solid with empty pockets

The inverse model fills the complete protein convex envelope and subtracts
the union of the eleven pocket probe meshes. Overlapping regions are removed
once. The outer envelope and the probe spaces retain their original scale.
The model is available for both common conformations and for the six
per-replica representatives.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/protein_solid_group_1_dark.png">
  <img src="images/protein_solid_group_1.png" width="100%" alt="Group 1: pocket positions, a cut through the inverse protein solid, and a detailed section through the empty heme cavity">
</picture>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/protein_solid_group_2_dark.png">
  <img src="images/protein_solid_group_2.png" width="100%" alt="Group 2: pocket positions, a cut through the inverse protein solid, and a detailed section through the empty heme cavity">
</picture>

The blue material is the filled envelope; green marks cavity walls. The detail
shows an exact planar section through the heme probe center. The complete
solid retains all cavities, including those outside this display section.
An enclosed cavity is visible after cutting the model or hiding its outer wall.

| File | Group 1 | Group 2 |
|---|---|---|
| `protein_solid` - complete envelope with empty pockets | [OBJ](structures/representative/whole_protein/protein_solid.obj), [PDB](structures/representative/whole_protein/protein_solid.pdb) | [OBJ](structures/representative/whole_protein_group_2/protein_solid.obj), [PDB](structures/representative/whole_protein_group_2/protein_solid.pdb) |
| `protein_section` - solid cut through the heme region | [OBJ](structures/representative/whole_protein/protein_section.obj) | [OBJ](structures/representative/whole_protein_group_2/protein_section.obj) |
| `pocket_voids` - union of the subtracted spaces | [OBJ](structures/representative/whole_protein/pocket_voids.obj), [SDF](structures/representative/whole_protein/pocket_voids.sdf) | [OBJ](structures/representative/whole_protein_group_2/pocket_voids.obj), [SDF](structures/representative/whole_protein_group_2/pocket_voids.sdf) |

All three models also have PLY, MOL, SDF and MOL2 files. OBJ and PLY retain
the surface triangles. PDB contains virtual vertices and mesh connections.
The numerical volume checks are in [solid_models.csv](tables/solid_models.csv).

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
for the calculation. The lining-atom envelope is stored in `hull.*`.

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
  representative/
    whole_protein/          Principal protein frame, group 1
    whole_protein_group_2/  Alternative protein frame, group 2
    pocket_geometry/        One shape-selected frame per pocket
    mean_volume/            One frame near each mean pocket volume
  R1/                      Original per-replica representatives
  R2/
  R3/
tables/                    Volumes, source frames and methods
images/                    Transparent previews
```

Inside `R1/`, `R2/` and `R3/`, `cluster_1/` and `cluster_2/` contain
representatives of the same common protein groups, selected within each replica.
In `whole_protein/` and `whole_protein_group_2/`, each named pocket folder uses
the parent protein frame. In `pocket_geometry/` and `mean_volume/`, each pocket
folder also contains its own complete parent protein. All coordinates are in Å.

### Four components

| Name | Contents |
|---|---|
| `residues` | Complete lining residues with heavy atoms within 4 Å of a probe-mesh vertex |
| `probe` | Internal space accessible to the center of a 1.4 Å probe |
| `hull` | Convex envelope of the lining-residue heavy atoms |
| `protein_hull` | Convex envelope of the complete parent HSA |
| `anchors.pdb` | Fixed reference residues used to locate and align the physiological region |

`residues.pdb` follows the cavity boundary in the selected frame.
`anchors.pdb` contains the alignment reference for that region; the two
selections can differ. The probe measures cavity space. The pocket hull
encloses the surrounding atoms, so its volume is different from the probe volume.

### All component combinations

Every pocket folder contains all fifteen nonempty combinations of the four
components as PDB files. `both_hulls` means the pocket hull and the complete
protein hull together. Filenames use letters, numbers and underscores.

| Components | File stem |
|---|---|
| Residues | `residues` |
| Probe | `probe` |
| Pocket hull | `hull` |
| Protein hull | `protein_hull` |
| Residues + probe | `residues_probe` |
| Residues + pocket hull | `residues_hull` |
| Residues + protein hull | `residues_protein_hull` |
| Probe + pocket hull | `probe_hull` |
| Probe + protein hull | `probe_protein_hull` |
| Both hulls | `both_hulls` |
| Residues + probe + pocket hull | `residues_probe_hull` |
| Residues + probe + protein hull | `residues_probe_protein_hull` |
| Residues + both hulls | `residues_both_hulls` |
| Probe + both hulls | `probe_both_hulls` |
| Residues + probe + both hulls | `residues_probe_both_hulls` |

The seven combinations containing only geometry also have OBJ, PLY, MOL, SDF
and MOL2 exports. MOL/SDF/MOL2 encode mesh vertices as virtual atoms and edges
as geometric links. These files retain the cavity geometry for shape processing;
the chemical atoms and residue identities are in the atomic PDB files.
An empty probe file records a frame in which no space fits the selected probe.

### Complete protein models

| File | Contents |
|---|---|
| `protein.pdb` | Complete atomic parent protein |
| `protein_with_hull.pdb` | Protein atoms and complete protein hull |
| `protein_with_probe.pdb` | Protein atoms and one pocket probe; inside each pocket folder |
| `protein_with_probe_and_hull.pdb` | Protein atoms, one pocket probe and complete protein hull |
| `probes.*` | All eleven probe meshes from one coherent protein frame |
| `protein_with_probes.pdb` | Protein atoms and all eleven probes |
| `probes_protein_hull.*` | All probes and the complete protein hull |
| `protein_with_probes_and_hull.pdb` | Protein atoms, all probes and protein hull |
| `protein_solid.*` | Filled protein hull with the probe union removed |
| `protein_section.*` | Cutaway version of the inverse solid |
| `pocket_voids.*` | The union removed from the inverse solid |

The complete all-pocket models are in the two `whole_protein` folders and the
six `R1`-`R3` group folders. All fifteen pocket combinations and their paths
are listed in [model_files.csv](tables/model_files.csv).
Frame selections, clustering comparisons and table definitions are in
[Methods and numerical results](tables/README.md).

## License

The original structures, geometric models, numerical tables, figures and
documentation in this collection are licensed under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE).

Reuse and adaptation, including commercial use, are permitted with appropriate
credit, a link to the license and an indication of any changes. Please identify
this collection and retain the author and source information supplied with
the material.

Third-party material retains its original terms and attribution.
