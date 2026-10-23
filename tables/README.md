# Methods and numerical results

[Return to the structure collection](../README.md)

## Sampling and frame selection

The dataset contains three independent 1 µs trajectories of native 585-residue
HSA. Replica identity is retained throughout. Coordinates are in Å and volumes
in Å³. Display alignment affects preview images only; the delivered coordinates
and all original numerical tables are unchanged.

### Common whole-protein frame

Each saved frame is described by three measurements:

- **Domain I-III COM distance:** the distance between the domains' centers of mass.
- **Opening angle:** the angle between the centers of mass of Domains I, II and III, with Domain II at the vertex.
- **Q_I-III:** the fraction of reference contacts between Domains I and III retained in that frame.

The clustering compares overall opening geometries. Training uses 200 uniformly
sampled frames from each replica, giving 600 frames with equal replica weights.
Each measurement is centered on its training-set mean and divided by its
training-set SD, so distances, angles and contact fractions contribute on
comparable scales.

K-means, Ward and DBSCAN candidates were compared. The selected two-group
Ward model was fitted to the training set; all 30,000 saved frames were then
assigned to the nearest group center in the standardized measurements.
Group 1 contains 68.3% of these frames. Its representative is the observed
member closest to its group center: R3, frame 2726, at 27.26% of production.
All eleven pocket geometries in `whole_protein/` were computed from this
same frame. The selected frame summarizes the opening measurements; its
individual pocket volumes can differ from their trajectory means.

### Ward and DBSCAN comparison

Ward is agglomerative hierarchical clustering: each merge minimizes the increase
in within-group squared variation. DBSCAN uses a neighborhood radius, `eps`,
and minimum local sample count, `min_samples`, to identify dense regions and
leave sparse observations unassigned. K-means fits a specified number of centers.

The selection score is assigned training fraction multiplied by the nonnegative
silhouette. Candidates require at least five training observations per group.
This score evaluates both separation and sample coverage. It selected Ward with
two groups (silhouette 0.3824), followed by two-group k-means (0.3663).
The best eligible DBSCAN candidate has three groups, `eps = 0.4495` in standardized
feature units and `min_samples = 20`: silhouette 0.2931, coverage 68.17%, score
0.1998. Sparse frames account for 31.83% of its training sample.

The stored Ward assignments were reproduced for all 30,000 frames. The DBSCAN
training labels, coverage and silhouette were also reproduced. Extension of
the DBSCAN core neighborhoods to the full saved dataset leaves 32.99% unassigned.
Each frame is assigned to its nearest training core point when their distance
is within `eps`; otherwise it remains unassigned.
The comparison does not replace the original Ward representatives.
Results are in [protein_clustering_comparison.csv](protein_clustering_comparison.csv),
all candidates in [protein_clustering_candidates.csv](protein_clustering_candidates.csv),
and DBSCAN per-replica populations in
[protein_dbscan_populations.csv](protein_dbscan_populations.csv).
Algorithm definitions are available in the
[SciPy Ward documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.ward.html)
and the [scikit-learn DBSCAN guide](https://scikit-learn.org/stable/modules/clustering.html#dbscan).

### Second common whole-protein frame

The second group contains 31.7% of the equally weighted R1-R3 frames. Its
common observed representative is R2, frame 8894 (88.94% of production).
The eleven pocket geometries were extracted anew on that frame with the same
physiological regions, atomic exclusions and 1.4 Å probe used for group 1.
The cleft uses the existing common local lattice. These measurements are
reported in [second_group_models.csv](second_group_models.csv).

Group 2 is the less populated of the two common groups. Its frame fractions
are 30.2% in R1, 62.1% in R2 and 2.8% in R3. Thus the 31.7% pooled fraction also
contains substantial replica variability. The original common assignments and
source-frame tables are retained in
[common_cluster_populations.csv](common_cluster_populations.csv) and
[common_cluster_representatives.csv](common_cluster_representatives.csv).

The preview images align the two observed proteins on Domain II and use one
frontal view and molecular scale. Delivered model coordinates retain their
source-frame positions. Complete group 2 structures and geometry are in
[`structures/representative/whole_protein_group_2/`](../structures/representative/whole_protein_group_2).

### Independent pocket-shape frames

Each region was analyzed across 102 uniformly sampled frames per replica,
including the first and last saved frames: 306 observations per region. Local
Cα alignment places the probe-space masks on a common grid. Jaccard distance
compares occupied grid cells, allowing different shapes with equal volume to be
distinguished. The representative is the observed medoid: the member minimizing
the sum of its Jaccard distances to the other members of the dominant nonempty
group. The geometry and atomic coordinates belong to that observed frame.

Average-linkage partitions with two to six groups and DBSCAN candidates were
compared. Candidate groups require at least five frames or 5% of the nonempty
sample, whichever is larger. DBSCAN coverage must reach 70%. A partition is
retained if coverage × silhouette is at least 0.25; otherwise one nonempty
geometry group is used. The criteria retained two DBSCAN groups for FA5; the
other regions were each summarized by one nonempty shape ensemble.

Empty masks are recorded as group 0 and DBSCAN noise as −1. Positive group
numbers are ordered by population. The selected medoid can differ in volume
from the trajectory mean. Shape overlap and volume percentiles are reported in
[pocket_shape_representativeness.csv](pocket_shape_representativeness.csv).
Each pocket-specific frame retains its own complete source protein.

### Frames closest to the mean pocket volume

For each region, one additional observed frame minimizes the absolute difference
between its volume and the mean of the original 306 observations. Ties are
resolved by replica order and then by the earliest frame. These frames include
the same treatment of zero-volume observations as the reported MD mean.
The coordinates are taken directly from the selected frame. The mean describes
cavity size across the sampled ensemble; it does not define a unique cavity shape.

The selected models, complete parent proteins and geometric envelopes are in
[`mean_volume/`](../structures/representative/mean_volume). Source frames, exact
volumes and differences from the target means are in
[mean_volume_models.csv](mean_volume_models.csv). The cleft uses the original
moving landmark lattice for this selection, matching the trajectory-volume table.

## How the cavity geometry is extracted

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

`residues.pdb` contains the complete residues whose heavy atoms lie within
4 Å of a probe-mesh vertex in the selected frame. The selection follows the
actual cavity geometry and can change with conformation.

`anchors.pdb` contains the local alignment-anchor residues used to position
the physiological reference region on that frame. These fixed residue identities
are listed in `alignment_canonical_residues` in `pocket_shape_methods.csv`.
They provide a reference for locating the site; they can differ from its lining
residues.

A lining convex hull encloses those residues' heavy-atom positions. The complete
protein hull encloses the heavy atoms of the source protein. These envelopes bridge
concavities and differ from both an atomic solvent-excluded surface and the
probe-space mesh. The probe mesh retains the unsmoothed 1 Å calculation grid.

## Inverse whole-protein solids

The complete heavy-atom protein convex hull is converted to a closed triangular
solid. A Boolean union combines all nonempty physiological probe meshes from
that same frame. The union is clipped to the protein envelope and subtracted
from it. This preserves overlaps without double counting and retains the
original probe geometry at scale 1.0. No cavity smoothing or enlargement is used.

`protein_solid` contains the remaining material; `pocket_voids` contains the
space removed from it. The exterior is a convex envelope and bridges the
protein's external surface indentations.

All eight full solids were checked for closed surfaces and positive volume.
For each model, solid volume plus the clipped union volume reproduces the
starting hull volume. Boolean operations use Manifold3D 3.5.4 with
double-precision mesh coordinates; Trimesh 5.1.1 provides independent surface
and volume checks. Full measurements are in [solid_models.csv](solid_models.csv).

### Local cavity surroundings

`pocket_solid` isolates the selected cavity and a rounded part of its surrounding
solid. First, the pocket probe is subtracted from the convex hull of its own
parent protein. The local context is then limited to the convex envelope of
the probe, dilated by a nominal 10 Å spherical margin. The spherical buffer is
represented by a geodesic mesh with 32 circular segments. This buffer controls
only the displayed outer context; the original pocket space remains unchanged.
The local solid is clipped to the protein hull.

The construction is applied to all 110 pocket folders: 92 have nonempty cavity
space, while 18 retain empty local files. Each nonempty model was checked for a
closed surface and positive volume. The volume of the local material plus
its empty cavity reproduces the clipped local envelope volume, with a largest
numerical error below 0.000001 Å³. Source proteins, margin, status and measured
volumes are in [pocket_solid_models.csv](pocket_solid_models.csv).

The previews use transparent amber for the solid material and green for the
boundary of the empty cavity. They show the complete protein beside its heme
cavity as a local example. Common scales are retained across the two groups
within the whole-protein and local panels.

Full and local solids have OBJ, PLY, PDB, MOL, SDF and MOL2 exports. OBJ and PLY
retain indexed surface triangles. PDB mesh connections give a wireframe display
in molecular viewers. Separate coincident vertices are retained where grid-based
cavity surfaces touch. The geometry-only molecular formats retain virtual
vertices and mesh links.

## Component files and combinations

Each pocket has four components: its lining `residues`, internal `probe` space,
lining-residue `hull` and complete `protein_hull`. All fifteen nonempty subsets
are delivered as PDB files. `both_hulls` combines the two envelopes. The seven
pure-geometry subsets also have OBJ, PLY, MOL, SDF and MOL2 exports.
[model_files.csv](model_files.csv) records components, chemical-atom counts,
virtual-vertex counts, formats and paths for all 1,650 combinations.
Original protein atom records and coordinates are retained in every atomic model.

## What does “probe availability” mean in the CSV?

The `sampled_probe_availability` column in `representative_comparison.csv` is the
fraction of sampled frames in which the defined region contains any accessible
probe-center space. A value of 0.50 means the 1.4 Å probe fits within that region
in half of the sampled frames. It is not a measured ligand-binding probability.
A zero-volume observation can result from a narrow or occluded cavity under
this particular probe size and region definition. The physiological reference
region remains defined even when no probe fits.

The raw CSV field names are retained for reproducibility. The main summary
shows the volumes directly.

## Tables

| Table | Contents |
|---|---|
| [Volume summary](pocket_volume_summary.csv) | Mean and sample SD of the three replica means |
| [Per-replica volumes](per_replica_pocket_volumes.csv) | Mean, median and within-replica spread |
| [Sampled volumes](sampled_pocket_volumes.csv) | Original 102 frames per replica and region |
| [Original pocket models](pocket_models.csv) | Original 66 R1-R3 models and source frames |
| [Protein representatives](protein_representatives.csv) | Per-replica protein-cluster populations and frames |
| [Representative comparison](representative_comparison.csv) | Ensemble means and volumes of the two selected model sets |
| [Representative models](representative_models.csv) | Source frames, lining residues, populations and file locations |
| [Near-mean-volume models](mean_volume_models.csv) | Observed frames closest to the MD mean, their volumes and absolute differences |
| [Near-mean geometric formats](mean_volume_geometry_formats.csv) | Geometric exports of the near-mean-volume frames |
| [Shape assignments](pocket_shape_assignments.csv) | Geometry labels and volumes for all 306 observations per region |
| [Shape populations](pocket_shape_populations.csv) | Geometry-group populations by replica |
| [Clustering candidates](pocket_shape_candidates.csv) | Candidate partitions, silhouettes and coverage |
| [Pocket-shape methods](pocket_shape_methods.csv) | Alignment residues, grids and method for each region |
| [Shape representativeness](pocket_shape_representativeness.csv) | Medoid overlap and selected-volume percentile |
| [Representative geometry formats](representative_geometry_formats.csv) | Exported geometry files and vertex/face counts |
| [Second-group models](second_group_models.csv) | Pocket volumes, lining residues and source frame for common group 2 |
| [Second-group geometry formats](second_group_geometry_formats.csv) | Additional geometric exports for common group 2 |
| [Original geometry formats](geometry_formats.csv) | Original R1-R3 geometric exports |
| [Model files](model_files.csv) | All fifteen component combinations in every pocket folder |
| [Inverse solids](solid_models.csv) | Hull, empty-space union, remaining solid and volume checks |
| [Local pocket solids](pocket_solid_models.csv) | Rounded 10 Å surroundings, source frames and volume checks |
| [Protein clustering comparison](protein_clustering_comparison.csv) | Best eligible Ward, k-means and DBSCAN results |
| [Protein clustering candidates](protein_clustering_candidates.csv) | Original candidate comparison |
| [DBSCAN populations](protein_dbscan_populations.csv) | Full-dataset density groups and unassigned frames, by replica |

## Geometric export formats

MOL/SDF use V3000 and atomic number 0 (`*`) for vertices. MOL2 uses `Du`.
Mesh edges have no physical charge, chemical bond assignment or force-field
parameters. OBJ/PLY encode triangular faces directly; SDF and MOL2 also retain
face-index annotations. Readback checks compared the exported vertex positions,
edge graphs and face records. Actual protein atoms and their coordinates remain
in the atomic PDB files.

Source: `CATIONIZED_HSA/series_585_apbs`, native system 0%. Original trajectories,
probe masks, analysis code and calculation records remain on the cluster.

Preview camera settings, source hashes and the schematic overview are recorded
in [images/FIGURE_SOURCES.json](../images/FIGURE_SOURCES.json).
