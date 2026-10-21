# Methods and numerical results

[Return to the structure collection](../README.md)

## Sampling and frame selection

The dataset contains three independent 1 µs trajectories of native 585-residue
HSA. Replica identity is retained throughout. Coordinates are in Å and volumes
in Å³. Display alignment affects preview images only; the delivered coordinates
and all original numerical tables are unchanged.

### Common whole-protein frame

The common protein classification uses Domain I–III COM distance, opening angle
and Q_I–III with standardized features. Candidate k-means, Ward and DBSCAN
classifications were compared using equally sampled replicas. The selected Ward
classification contains two groups. The whole-protein frame is R3, frame 2726
(27.26% of production), from the dominant group containing 68.3% of all equally
weighted R1–R3 frames. All eleven geometries were recalculated on that same
observed frame. This classification describes overall opening coordinates.

### Independent pocket-shape frames

Each region was analyzed across 102 uniformly sampled frames per replica,
including the first and last saved frames: 306 observations per region. Local
Cα alignment places the probe-space masks on a common grid. Jaccard distance
compares occupied grid cells, allowing different shapes with equal volume to be
distinguished. The representative is the observed medoid: the member minimizing
the sum of its Jaccard distances to the other members of the dominant nonempty
group. It is not a coordinate average or a frame selected by mean volume.

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


Lining residues have heavy atoms within 4 Å of probe-mesh vertices. A lining
convex hull encloses those residues' heavy-atom positions. The complete protein
hull encloses the heavy atoms of the source protein. These envelopes bridge
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
| [Original pocket models](pocket_models.csv) | Original 66 R1–R3 models and source frames |
| [Protein representatives](protein_representatives.csv) | Per-replica protein-cluster populations and frames |
| [Representative comparison](representative_comparison.csv) | Ensemble means and volumes of the two selected model sets |
| [Representative models](representative_models.csv) | Source frames, lining residues, populations and file locations |
| [Shape assignments](pocket_shape_assignments.csv) | Geometry labels and volumes for all 306 observations per region |
| [Shape populations](pocket_shape_populations.csv) | Geometry-group populations by replica |
| [Clustering candidates](pocket_shape_candidates.csv) | Candidate partitions, silhouettes and coverage |
| [Pocket-shape methods](pocket_shape_methods.csv) | Alignment residues, grids and method for each region |
| [Shape representativeness](pocket_shape_representativeness.csv) | Medoid overlap and selected-volume percentile |
| [Representative geometry formats](representative_geometry_formats.csv) | Exported geometry files and vertex/face counts |
| [Original geometry formats](geometry_formats.csv) | Original R1–R3 geometric exports |

## Geometric export formats

MOL/SDF use V3000 and atomic number 0 (`*`) for vertices. MOL2 uses `Du`.
Mesh edges have no physical charge, chemical bond assignment or force-field
parameters. OBJ/PLY encode triangular faces directly; SDF and MOL2 also retain
face-index annotations. Readback checks compared the exported vertex positions,
edge graphs and face records. Actual protein atoms and their coordinates remain
in the atomic PDB files.

Source: `CATIONIZED_HSA/series_585_apbs`, native system 0%. Original trajectories,
probe masks, analysis code and calculation records remain on the cluster.
