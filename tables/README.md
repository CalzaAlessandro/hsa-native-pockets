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

`pocket_atoms.pdb` contains the complete residues whose heavy atoms lie within
4 Å of a probe-mesh vertex in the selected frame. The selection follows the
actual cavity geometry and can change with conformation.

`region_atoms.pdb` contains the local alignment-anchor residues used to position
the physiological reference region on that frame. These fixed residue identities
are listed in `alignment_canonical_residues` in `pocket_shape_methods.csv`.
They provide a reference for locating the site; they can differ from its lining
residues.

A lining convex hull encloses those residues' heavy-atom positions. The complete
protein hull encloses the heavy atoms of the source protein. These envelopes bridge
concavities and differ from both an atomic solvent-excluded surface and the
probe-space mesh. The probe mesh retains the unsmoothed 1 Å calculation grid.

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
