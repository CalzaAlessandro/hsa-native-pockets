# Data and methods reference

[Back to README](../README.md).

## Pocket volumes

**MD mean ± SD** reports the average of the three replica means and their
between-replica SD. Each replica mean includes all 102 sampled observations,
including frames with zero accessible probe space.

**Dominant protein** and **Alternative protein** give the volumes in the two
whole-protein frames.
**Pocket shape** gives the volume in the frame selected by cavity geometry.

**Mean volume** gives the cavity volume in the observed frame closest to the
MD mean among the 306 sampled frames. Its model is in
[`mean_volume/`](../structures/representative/mean_volume). All volumes are in Å³.

| Pocket | MD mean ± SD | Dominant protein | Alternative protein | Pocket shape | Mean volume |
|---|---:|---:|---:|---:|---:|
| Sudlow&nbsp;I | 65.9 ± 13.4 | [50](../structures/representative/whole_protein/Sudlow_I) | [55](../structures/representative/whole_protein_group_2/Sudlow_I) | [114](../structures/representative/pocket_geometry/Sudlow_I) | [66](../structures/representative/mean_volume/Sudlow_I) |
| Sudlow&nbsp;II | 16.4 ± 10.6 | [24](../structures/representative/whole_protein/Sudlow_II) | [3](../structures/representative/whole_protein_group_2/Sudlow_II) | [36](../structures/representative/pocket_geometry/Sudlow_II) | [16](../structures/representative/mean_volume/Sudlow_II) |
| Heme | 173.5 ± 36.9 | [136](../structures/representative/whole_protein/Heme) | [63](../structures/representative/whole_protein_group_2/Heme) | [383](../structures/representative/pocket_geometry/Heme) | [174](../structures/representative/mean_volume/Heme) |
| Cleft | 233.5 ± 103.8 | [250](../structures/representative/whole_protein/Cleft) | [392](../structures/representative/whole_protein_group_2/Cleft) | [307](../structures/representative/pocket_geometry/Cleft) | [231](../structures/representative/mean_volume/Cleft) |
| FA1 | 41.0 ± 13.1 | [0](../structures/representative/whole_protein/FA1) | [60](../structures/representative/whole_protein_group_2/FA1) | [129](../structures/representative/pocket_geometry/FA1) | [41](../structures/representative/mean_volume/FA1) |
| FA2 | 5.7 ± 4.6 | [1](../structures/representative/whole_protein/FA2) | [0](../structures/representative/whole_protein_group_2/FA2) | [11](../structures/representative/pocket_geometry/FA2) | [6](../structures/representative/mean_volume/FA2) |
| FA3 | 4.2 ± 4.4 | [0](../structures/representative/whole_protein/FA3) | [3](../structures/representative/whole_protein_group_2/FA3) | [3](../structures/representative/pocket_geometry/FA3) | [4](../structures/representative/mean_volume/FA3) |
| FA4 | 57.9 ± 33.2 | [53](../structures/representative/whole_protein/FA4) | [36](../structures/representative/whole_protein_group_2/FA4) | [120](../structures/representative/pocket_geometry/FA4) | [58](../structures/representative/mean_volume/FA4) |
| FA5 | 14.1 ± 15.0 | [26](../structures/representative/whole_protein/FA5) | [1](../structures/representative/whole_protein_group_2/FA5) | [38](../structures/representative/pocket_geometry/FA5) | [14](../structures/representative/mean_volume/FA5) |
| FA6 | 169.1 ± 24.5 | [168](../structures/representative/whole_protein/FA6) | [181](../structures/representative/whole_protein_group_2/FA6) | [199](../structures/representative/pocket_geometry/FA6) | [169](../structures/representative/mean_volume/FA6) |
| FA7 | 9.3 ± 5.5 | [2](../structures/representative/whole_protein/FA7) | [0](../structures/representative/whole_protein_group_2/FA7) | [25](../structures/representative/pocket_geometry/FA7) | [9](../structures/representative/mean_volume/FA7) |

A zero means that the 1.4 Å probe has no accessible center positions within
the specified region in that frame. FA7 overlaps Sudlow I, and FA3/FA4 overlap
Sudlow II.

- [Full comparison table](../tables/representative_comparison.csv)
- [Source frames and lining residues](../tables/representative_models.csv)
- [Mean-volume frames](../tables/mean_volume_models.csv)
- [Methods and table definitions](../tables/README.md)

## Find the files

```text
structures/
├── representative/
│   ├── whole_protein/          Dominant protein frame
│   ├── whole_protein_group_2/  Alternative protein frame
│   ├── pocket_geometry/        One shape-selected frame per pocket
│   └── mean_volume/            One frame near each mean pocket volume
├── R1/                        Per-replica representatives
├── R2/
└── R3/
tables/                        Volumes, source frames and methods
images/                        Transparent previews
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

Probe volume measures accessible internal space. The pocket hull encloses
the lining atoms.

### All component combinations

Every pocket folder contains all fifteen nonempty combinations of the four
components as PDB files. `both_hulls` means the pocket hull and the complete
protein hull together.

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
as geometric links. Atomic PDB files contain the chemical atoms and residue
identities.
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
| `pocket_solid.*` | One empty cavity with rounded 10 Å solid surroundings; inside each pocket folder |
| `pocket_voids.*` | The union removed from the inverse solid |

Local solids are available for all nonempty pockets in every model collection.
An empty local file records a frame with no accessible probe space.

The complete all-pocket models are in the two `whole_protein` folders and the
six `R1`-`R3` group folders. [model_files.csv](../tables/model_files.csv) lists the
components and paths for all pocket combinations.

## Software and references

| Software / model | Role | Primary reference |
|---|---|---|
| [Amber](https://ambermd.org/) / ff14SB | Production molecular dynamics of native 585-residue HSA | Case et al., *J. Chem. Inf. Model.* 2023 ([10.1021/acs.jcim.3c01153](https://doi.org/10.1021/acs.jcim.3c01153)); Maier et al., *J. Chem. Theory Comput.* 2015 ([10.1021/acs.jctc.5b00255](https://doi.org/10.1021/acs.jctc.5b00255)) |
| [SciPy](https://scipy.org/) | Hierarchical Ward clustering and convex-hull geometry | Virtanen et al., *Nat. Methods* 2020 ([10.1038/s41592-019-0686-2](https://doi.org/10.1038/s41592-019-0686-2)) |
| [scikit-learn](https://scikit-learn.org/) | *k*-means, DBSCAN and silhouette evaluation | Pedregosa et al., *J. Mach. Learn. Res.* 2011 ([jmlr.org/papers/v12/pedregosa11a.html](https://jmlr.org/papers/v12/pedregosa11a.html)) |
| [Manifold](https://github.com/elalish/manifold) / [Trimesh](https://trimesh.org/) | Exact Boolean solid operations and closed-surface validation | Manifold3D & Trimesh |
| [VMD](https://www.ks.uiuc.edu/Research/vmd/) / Tachyon | Molecular visualization and ray-traced figures | Humphrey, Dalke & Schulten, *J. Mol. Graph.* 1996 ([10.1016/0263-7855(96)00018-5](https://doi.org/10.1016/0263-7855(96)00018-5)) |
