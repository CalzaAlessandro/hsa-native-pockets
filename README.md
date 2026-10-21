# Native HSA physiological pockets

Pocket structures and geometric models from three independent 1 µs trajectories
of **585-residue native HSA**. The R1–R3 results are retained, together with one
common whole-protein template and independently selected pocket-shape templates.

## Two representative models

| Model | Selection | Use |
|---|---|---|
| [Whole-protein representative](structures/representative/whole_protein) | Observed frame closest to the center of the dominant common protein cluster | Position all physiological pockets within one HSA conformation |
| [Pocket-shape representatives](structures/representative/pocket_geometry) | Observed medoid of the dominant nonempty geometry group for each pocket | Inspect local cavity geometry independently of overall HSA opening |

The whole-protein template is **R3, frame 2726 (27.26%
of production)**. Its protein cluster contains 68.3% of the equally
weighted R1–R3 frames. All eleven pocket geometries in this template were
calculated on that same frame.

For the pocket-shape templates, each region was analyzed separately across
102 uniformly sampled frames from each replica, giving 306 frames per region.
Local Cα alignment places its probe-space masks on the same grid. Jaccard
distance compares the occupied grid cells and distinguishes different shapes
with equal volume. Average-linkage clustering and DBSCAN candidates were
compared; the selected geometry is an actual member nearest the other members
of the most populated nonempty group. A single group is retained when the
candidate partitions have low silhouette scores. Each local template has its
own source protein, frame and geometric envelope.

These criteria retained two DBSCAN groups for FA5. The remaining regions were
summarized by one nonempty shape ensemble each. The medoid is chosen by spatial
overlap and its volume can differ from the trajectory mean. The
[representativeness table](tables/pocket_shape_representativeness.csv) reports
shape overlap and the position of each selected volume within its sampled
distribution.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/HSA_common_representative_dark.png">
  <img src="images/HSA_common_representative.png" width="100%" alt="Whole-protein envelope with all physiological probes">
</picture>

[Whole-protein PDB](structures/representative/whole_protein/protein.pdb) ·
[Atomic protein and all probes](structures/representative/whole_protein/HSA_with_all_pockets.pdb) ·
[Protein hull and all probes, PDB](structures/representative/whole_protein/HSA_hull_with_all_pockets.pdb) ·
[OBJ](structures/representative/whole_protein/HSA_hull_with_all_pockets.obj) ·
[SDF](structures/representative/whole_protein/HSA_hull_with_all_pockets.sdf)

## Pocket volumes and models

Trajectory summaries are the mean ± sample SD of the three replica means.
The two model columns give the volume in the selected observed frame. Click a
model volume to open its structure folder. Probe availability is the fraction
of the 306 sampled frames with nonzero probe-center space in the defined region.
The local shape template is selected from those nonempty frames.

| Region | Trajectory mean ± SD (Å³) | Whole-protein model (Å³) | Pocket-shape model (Å³) | Probe availability |
|---|---:|---:|---:|---:|
| Cleft | 233.5 ± 103.8 | [250](structures/representative/whole_protein/Cleft) | [307](structures/representative/pocket_geometry/Cleft) | 100.0% |
| FA1 | 41.0 ± 13.1 | [0](structures/representative/whole_protein/FA1) | [129](structures/representative/pocket_geometry/FA1) | 83.7% |
| FA2 | 5.7 ± 4.6 | [1](structures/representative/whole_protein/FA2) | [11](structures/representative/pocket_geometry/FA2) | 46.1% |
| FA3 | 4.2 ± 4.4 | [0](structures/representative/whole_protein/FA3) | [3](structures/representative/pocket_geometry/FA3) | 42.5% |
| FA4 | 57.9 ± 33.2 | [53](structures/representative/whole_protein/FA4) | [120](structures/representative/pocket_geometry/FA4) | 98.7% |
| FA5 | 14.1 ± 15.0 | [26](structures/representative/whole_protein/FA5) | [38](structures/representative/pocket_geometry/FA5) | 64.4% |
| FA6 | 169.1 ± 24.5 | [168](structures/representative/whole_protein/FA6) | [199](structures/representative/pocket_geometry/FA6) | 100.0% |
| FA7 | 9.3 ± 5.5 | [2](structures/representative/whole_protein/FA7) | [25](structures/representative/pocket_geometry/FA7) | 51.3% |
| Heme | 173.5 ± 36.9 | [136](structures/representative/whole_protein/Heme) | [383](structures/representative/pocket_geometry/Heme) | 99.3% |
| Sudlow I | 65.9 ± 13.4 | [50](structures/representative/whole_protein/Sudlow_I) | [114](structures/representative/pocket_geometry/Sudlow_I) | 98.4% |
| Sudlow II | 16.4 ± 10.6 | [24](structures/representative/whole_protein/Sudlow_II) | [36](structures/representative/pocket_geometry/Sudlow_II) | 63.7% |

[Comparison table](tables/representative_comparison.csv) ·
[Source frames, lining residues and models](tables/representative_models.csv) ·
[Geometry-cluster populations by replica](tables/pocket_shape_populations.csv)

### Heme

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/Heme_representatives_dark.png">
  <img src="images/Heme_representatives.png" width="100%" alt="Heme residues, probe and convex envelope in the two representative models">
</picture>

[Whole-protein-frame model](structures/representative/whole_protein/Heme) ·
[Pocket-shape model](structures/representative/pocket_geometry/Heme)

### FA6

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/FA6_representatives_dark.png">
  <img src="images/FA6_representatives.png" width="100%" alt="FA6 residues, probe and convex envelope in the two representative models">
</picture>

[Whole-protein-frame model](structures/representative/whole_protein/FA6) ·
[Pocket-shape model](structures/representative/pocket_geometry/FA6)

### Sudlow I

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="images/Sudlow_I_representatives_dark.png">
  <img src="images/Sudlow_I_representatives.png" width="100%" alt="Sudlow I residues, probe and convex envelope in the two representative models">
</picture>

[Whole-protein-frame model](structures/representative/whole_protein/Sudlow_I) ·
[Pocket-shape model](structures/representative/pocket_geometry/Sudlow_I)

Green shows the space available to probe centers; sticks show actual pocket-lining
atoms. The pale envelope is their convex hull. Both panels for one pocket use the
same scale and a local Cα fit to the same reference. Scale bars are 5 Å.

## Files

```text
tables/
structures/
├── representative/
│   ├── whole_protein/       One HSA frame, with all eleven pockets
│   └── pocket_geometry/     One independently chosen frame per pocket
├── R1/                     Original protein-cluster models
├── R2/
└── R3/
images/
```

The whole-protein folder contains `protein.pdb`, `protein_hull` models and one
subfolder per physiological region. Each local pocket folder contains its own
`protein.pdb`, `protein_hull` and the pocket files below. Coordinates are in Å.

| File | Contents |
|---|---|
| `pocket_atoms.pdb` | Actual lining residues within 4 Å of the probe-mesh vertices |
| `region_atoms.pdb` | The physiological reference-region residues |
| `probe.pdb`, `.obj`, `.ply` | Accessible probe-center geometry |
| `lining_hull.pdb`, `.obj`, `.ply` | Convex envelope of the lining-residue heavy atoms |
| `pocket_with_geometry.pdb` | Lining atoms, probe model and complete protein hull |
| `protein_with_pocket.pdb` | Complete atomic protein with that pocket and protein hull |
| `protein_hull.pdb`, `.obj`, `.ply` | Convex envelope of the complete protein |

Every OBJ also has `.sdf`, `.mol` and `.mol2` exports. These geometric files use
virtual vertices: `*` in MOL/SDF and `Du` in MOL2. Mesh edges carry no chemical
bond types, physical charges or force-field parameters. MOL/SDF use V3000.
OBJ/PLY retain triangular faces; SDF and MOL2 additionally record face indices.
Actual protein atoms remain in the PDB files.

[Representative geometry formats](tables/representative_geometry_formats.csv) ·
[Original R1–R3 geometry formats](tables/geometry_formats.csv)

## Replicas and numerical results

The original R1, R2 and R3 structures and results are unchanged. Each replica
retains two whole-protein cluster representatives, with all eleven regions
calculated on the corresponding observed frame.

| Table | Contents |
|---|---|
| [Volume summary](tables/pocket_volume_summary.csv) | Mean and SD of the three replica means |
| [Per-replica volumes](tables/per_replica_pocket_volumes.csv) | Mean, median and spread within each replica |
| [Sampled volumes](tables/sampled_pocket_volumes.csv) | Original 102 sampled frames per replica and region |
| [Original pocket models](tables/pocket_models.csv) | The 66 R1–R3 models and source frames |
| [Protein representatives](tables/protein_representatives.csv) | Original protein-cluster populations and frames |
| [Pocket-shape assignments](tables/pocket_shape_assignments.csv) | Local geometry labels and volumes for all 306 sampled frames |
| [Clustering candidates](tables/pocket_shape_candidates.csv) | Candidate partitions, silhouettes and coverage |
| [Pocket-shape methods](tables/pocket_shape_methods.csv) | Alignment residues, grids and selected method for each site |

## Extraction

Experimental ligand positions define the physiological regions. Local canonical
Cα anchors transfer those regions onto each observed frame. Protein atoms
exclude space using element-specific radii. A 1.4 Å spherical probe and a
1 Å grid measure seed-connected free space inside each ligand-informed region.
Heme uses the hemin region from 1O9X. The cleft uses free space inside its moving
residue-landmark convex envelope.

The new cleft shape comparison uses a common grid after local landmark
alignment. The original trajectory-volume table retains its original moving-grid
measurement. Protein and lining hulls enclose atomic positions; the green probe
mesh describes the available cavity space. FA7 overlaps Sudlow I; FA3 and FA4
overlap Sudlow II, so these region volumes should not be summed.

Shape clustering includes nonempty masks. Empty masks are recorded as group 0
and DBSCAN noise as −1. Positive group numbers are ordered by population.
Candidate groups require at least five frames or 5% of the nonempty sample,
whichever is larger. DBSCAN coverage must reach 70%; the selected partition
maximizes coverage × silhouette with a minimum score of 0.25. Otherwise one
shape group is retained. These sampled populations describe this geometric
classification; replica identity remains available in every assignment table.

Source: `CATIONIZED_HSA/series_585_apbs`, native system 0%. Original trajectories,
analysis code, probe masks and full calculation records remain on the cluster.
