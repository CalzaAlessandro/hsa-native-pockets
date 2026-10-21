# Native HSA pocket templates

Three independent 1 µs trajectories, full-length 585-residue HSA at pH 7.4.
Each folder contains one actual whole-protein cluster representative. All
pockets in that folder are recalculated on the same frame, never on averaged
coordinates. Clusters use standardized domain I–III distance, opening angle
and native-contact fraction, comparing k-means, Ward and DBSCAN on equally
sampled replicas. Cluster populations and frame identities remain explicit.

Physiological regions use the experimental ligand-informed sphere unions
transferred to this native model by canonical local C-alpha alignment. Heme
uses the 1O9X ligand. The cleft is moving landmark-bounded open space.
Protein atoms exclude space with documented element radii; the spherical
probe radius is 1.4 Å and the grid spacing is 1 Å. FA7/Sudlow I and FA3/FA4/
Sudlow II overlap and must not be added as independent volumes. Boundary
contact records possible region truncation. Protein/lining hulls describe
occupied-atom envelopes; they are separate from probe-accessible space.

PDBs contain real protein atoms, extracted lining residues or disconnected
display geometry as named. OBJ/PLY are triangular meshes in the same Å
coordinates. HSA_with_all_pockets.pdb and HSA_hull_with_all_pockets.obj retain
the whole protein context. Canonical residue numbering is 1–585 throughout.
MDpocket detection-frequency/density and persistence results are separate
ensemble outputs under detected/, with per-replica identities retained.

Pocket-volume summaries use equal weighting of three replica means and
their sample SD. The 102 sampled frames per replica span 0.1–1000 ns;
they describe geometry/persistence at 9.9 ns intervals, not binding affinity.
