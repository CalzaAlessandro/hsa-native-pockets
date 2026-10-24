# Methods and numerical results

[Return to the structure collection](../README.md)

## Sampling and frame selection

Three independent 1 µs simulations of native, 585-residue HSA supplied 10,000
saved frames per replica. Coordinates are in Å and volumes in Å³.

### Whole-protein representatives

Protein opening was described by three measurements:

- Domain I-III center-of-mass distance.
- The angle between the centers of mass of Domains I, II and III, with Domain II at the vertex.
- Q_I-III, the fraction of native contacts retained between Domains I and III.

Clustering used 200 uniformly sampled frames per replica, giving 600 frames
with equal replica weights. Each measurement was centered on its training-set
mean and divided by its training-set SD. Ward, k-means and DBSCAN candidates
were compared on these standardized features. All 30,000 saved frames were assigned to the
nearest center of the selected two-group Ward model.

For each group, the observed frame closest to its center was selected.
Group 1 contained 68.3% of the frames; its representative was R3, frame 2726
(27.26% of production). Group 2 contained 31.7%; its representative was R2,
frame 8894 (88.94% of production). All eleven pocket geometries were calculated
on each selected protein frame using the same physiological regions, atomic
exclusions and 1.4 Å probe.

Group 2 populations were 30.2% in R1, 62.1% in R2 and 2.8% in R3.
Populations and selected frames are reported in
[common_cluster_populations.csv](common_cluster_populations.csv) and
[common_cluster_representatives.csv](common_cluster_representatives.csv).
Pocket measurements for the alternative conformation are in
[second_group_models.csv](second_group_models.csv).

### Clustering comparison

Ward clustering minimizes the increase in within-group squared variation at
each merge. K-means fits group centers. DBSCAN identifies dense regions using
a neighborhood radius, `eps`, and minimum neighbor count, `min_samples`.

Candidates required at least five training frames per group and were ranked
by assigned training fraction multiplied by the nonnegative silhouette score.
Ward with two groups scored 0.3824, followed by two-group k-means at 0.3663.
The best eligible DBSCAN candidate had three groups, `eps = 0.4495` in
standardized feature space and `min_samples = 20`: silhouette 0.2931,
assigned fraction 68.17% and score
0.1998. It left 31.83% of the training frames unassigned.

The DBSCAN model was extended to all saved frames by assigning each frame
to the nearest training core point within `eps`. This left 32.99% of frames
unassigned. Scores and settings are in
[protein_clustering_comparison.csv](protein_clustering_comparison.csv) and
[protein_clustering_candidates.csv](protein_clustering_candidates.csv);
per-replica DBSCAN populations are in
[protein_dbscan_populations.csv](protein_dbscan_populations.csv).
The algorithm definitions are described in the
[SciPy Ward documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.ward.html)
and [scikit-learn DBSCAN documentation](https://scikit-learn.org/stable/modules/clustering.html#dbscan).

### Pocket-shape representatives

Each pocket was sampled at 102 uniformly spaced frames per replica, including
the first and last saved frames, giving 306 observations. Local Cα alignment
placed cavity masks on a common 1 Å grid. Jaccard distance measured differences
in occupied grid cells. The representative was the medoid of the largest
nonempty group: the observed frame with the smallest sum of Jaccard distances
to the other group members.

Average-linkage partitions with two to six groups and DBSCAN candidates were
compared. Groups required at least five frames or 5% of the nonempty sample,
whichever was larger. DBSCAN candidates required at least 70% coverage.
Partitions were retained when coverage × silhouette was at least 0.25;
otherwise all nonempty masks formed one group. These criteria selected two
DBSCAN groups for FA5 and one nonempty group for each of the other pockets.

Empty masks were labeled 0 and DBSCAN noise −1. Positive group labels were
ordered by population. Medoid overlap and volume percentiles are reported in
[pocket_shape_representativeness.csv](pocket_shape_representativeness.csv).

### Mean-volume representatives

For each pocket, the selected frame minimized the absolute difference between
its volume and the mean over the 306 sampled observations, including zero
volumes. Ties were resolved by replica order and then the earliest frame.
The cleft calculation used the moving landmark lattice used for the trajectory
volume measurements. Selected frames, volumes and differences from the means
are in [mean_volume_models.csv](mean_volume_models.csv).

## Cavity extraction

Experimental ligand positions defined the physiological regions. Local
canonical Cα anchors transferred each region onto the sampled protein frames.
Protein atoms excluded space using element-specific radii. A 1.4 Å spherical
probe on a 1 Å grid measured seed-connected free space within each region.
The heme region was defined from hemin in 1O9X. The cleft was bounded by a
convex envelope of residue landmarks.

Cleft shapes were compared on a common grid after local landmark alignment;
trajectory cleft volumes were measured on a moving landmark grid. FA7 overlaps
Sudlow I, and FA3 and FA4 overlap Sudlow II, so these volumes are not additive.

Lining residues were selected from heavy atoms within 4 Å of a probe-mesh
vertex. Their complete residues are stored in `residues.pdb`. The fixed local
alignment residues are stored in `anchors.pdb` and listed under
`alignment_canonical_residues` in [pocket_shape_methods.csv](pocket_shape_methods.csv).

Pocket hulls were calculated from the lining-residue heavy atoms; protein
hulls were calculated from all protein heavy atoms. A convex hull bridges
surface concavities. Probe meshes follow the unsmoothed 1 Å grid.

## Protein and local cavity solids

The complete protein heavy-atom convex hull was converted to a closed
triangular solid. A Boolean union combined the nonempty pocket probe meshes
from that frame. The union was clipped to the protein hull and subtracted
at the calculated probe scale. Overlapping probe spaces were subtracted once.
The remaining material is stored in `protein_solid`; the removed space is
stored in `pocket_voids`.

All eight protein solids were checked for closed surfaces and positive
volume. Solid volume plus clipped cavity volume reproduced the starting
hull volume. Boolean operations used Manifold3D 3.5.4 with double-precision
coordinates; Trimesh 5.1.1 provided surface and volume checks. Measurements
are in [solid_models.csv](solid_models.csv).

### Local cavity surroundings

For each pocket, the probe mesh was subtracted from its parent protein hull.
The surrounding solid was limited to the probe's convex envelope expanded
by a nominal 10 Å spherical margin, represented by a polygonal sphere with
32 circular segments, and clipped to the protein hull.

Of the 110 pocket frames, 92 had nonempty probe space and produced local
solids; 18 had no accessible probe space. Each nonempty model was checked for
a closed surface and positive volume. Local solid volume plus cavity volume
reproduced the clipped local envelope volume with an error below 0.000001 Å³.
Source frames and measurements are in
[pocket_solid_models.csv](pocket_solid_models.csv).

For visual comparison, models were aligned on local Cα anchors and shown
with the same view and scale within each pocket. Amber marks solid material;
green marks the empty cavity boundary.

## Probe accessibility

The `sampled_probe_availability` field in
[representative_comparison.csv](representative_comparison.csv) reports the
fraction of sampled frames with nonzero accessible probe space. A value of
0.50 means that the 1.4 Å probe fits within the defined region in half of the
sampled frames. Zero volume indicates no accessible probe-center positions
under the selected probe size and region definition.

## Tables

| Table | Contents |
|---|---|
| [Volume summary](pocket_volume_summary.csv) | Mean and sample SD of the three replica means |
| [Per-replica volumes](per_replica_pocket_volumes.csv) | Mean, median and within-replica spread |
| [Sampled volumes](sampled_pocket_volumes.csv) | 102 sampled frames per replica and region |
| [Per-replica pocket models](pocket_models.csv) | 66 R1-R3 models and source frames |
| [Protein representatives](protein_representatives.csv) | Per-replica protein-cluster populations and frames |
| [Representative comparison](representative_comparison.csv) | Ensemble means and volumes of the two selected model sets |
| [Representative models](representative_models.csv) | Source frames, lining residues, populations and file locations |
| [Mean-volume models](mean_volume_models.csv) | Observed frames closest to the MD mean, their volumes and absolute differences |
| [Mean-volume geometric formats](mean_volume_geometry_formats.csv) | Geometric exports of the mean-volume frames |
| [Shape assignments](pocket_shape_assignments.csv) | Geometry labels and volumes for all 306 observations per region |
| [Shape populations](pocket_shape_populations.csv) | Geometry-group populations by replica |
| [Clustering candidates](pocket_shape_candidates.csv) | Candidate partitions, silhouettes and coverage |
| [Pocket-shape methods](pocket_shape_methods.csv) | Alignment residues, grids and method for each region |
| [Shape representativeness](pocket_shape_representativeness.csv) | Medoid overlap and selected-volume percentile |
| [Representative geometry formats](representative_geometry_formats.csv) | Exported geometry files and vertex/face counts |
| [Second-group models](second_group_models.csv) | Pocket volumes, lining residues and source frame for common group 2 |
| [Second-group geometry formats](second_group_geometry_formats.csv) | Additional geometric exports for common group 2 |
| [Per-replica geometry formats](geometry_formats.csv) | R1-R3 geometric exports |
| [Model files](model_files.csv) | All fifteen component combinations in every pocket folder |
| [Inverse solids](solid_models.csv) | Hull, empty-space union, remaining solid and volume checks |
| [Local pocket solids](pocket_solid_models.csv) | Rounded 10 Å surroundings, source frames and volume checks |
| [Protein clustering comparison](protein_clustering_comparison.csv) | Best eligible Ward, k-means and DBSCAN results |
| [Protein clustering candidates](protein_clustering_candidates.csv) | Candidate scores and settings |
| [DBSCAN populations](protein_dbscan_populations.csv) | Full-dataset density groups and unassigned frames, by replica |

## Geometric export formats

OBJ and PLY store indexed triangular surfaces. PDB stores mesh vertices and
connections. MOL and SDF use V3000 with atomic number 0 (`*`) for vertices;
MOL2 uses `Du`. SDF and MOL2 also store face indices. Separate coincident
vertices were retained where grid-based cavity surfaces touched.

Mesh vertices and edges describe geometry and have no chemical charge or
force-field parameters. Chemical atoms and residue identities are stored in
the atomic PDB files. Exports were checked by comparing vertex positions,
edge graphs and face records after readback.

The fifteen component combinations are listed in
[model_files.csv](model_files.csv), with 1,650 model records.
Figure sources and camera settings are in
[FIGURE_SOURCES.json](../images/FIGURE_SOURCES.json).
