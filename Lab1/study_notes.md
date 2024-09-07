<ins>ml summer school-day 1</ins>

equivariance and invariance

equivariance = output undergo exactly the same tranformation as applied to the input

invariance = output stay constant regardless of the applied transformation


equivariance is used in
- protein folding
- protein docking
- molucular dynamics
- solid state physics
- molecular electron densities
- cosmology, medical images and others

equivariance == data efficient (Nequip: Simon Batzner et al. 2021)

<ins>group and representations</ins>

group = operations and how they compose = rotations, parity

a Group, G follows the rules
- identity
- associativity
- inverse

representations = vector spaces on which the action of the group is defined = scalars, vectors, pseudovectors

a representation D(g, x) follows the rules:
- g member of G, x member of V
- Linear D(g, x + y) = D(g, x) + D(g, y)
- follow the structure of the group D(gh, x) = D(g, D(h,x))

f is equivariant if for all values of x \
f(D(g)x) = D^'(g)f(x)

<ins>mathematical properties of equivariant functions</ins>

f (V1 -> V2) and h (V2 -> V3)\
if f and h are equivariant functions, 
-  composition\
then h o f is equivariant\
h(f(D1(g)x)) = h(D2(g)f(x)) = D3(g)h(f(x)
- h + f is equivariant\
f(D1(g)x) + h(D2(g)x) = D3(g)(f(x) + h(x))
- a scalar alpha, member of R\
alpha * f is equivariant\
alpha*f(D1(g)x) = D2(g)alpha*f(x)

\
common data splitting techniques in drug discovery
- random splitting
- scaffold-based splitting - based on molecular scaffolds (core structures) of the compounds
- temporal splitting - 
- activity-based splitting - ensures compounds with a range of activities are present in both training and tests
- cluster-based splitting - group similiar compounds using clustering algos


choice of splitting approach:
- stage and purpose of the drug discovery program
- the structural diversity of the dataset
- the xteristics of the deployment set to which the predictive model will be applied


<ins>fingerprints</ins>
http://www.dalkescientific.com/writings/NBN/fingerprints.html

a chem fingerprint is a list of bin values which characterize a molecule
 the MACCS keys are a set of questions about the chem structure of a molecule whose answers are encoded in a list of bin values called the MACCS key fingerprint

 the hamming distance between 2 bitstrings make comparing fingerprints fast and easy

 https://www.daylight.com/dayhtml/doc/theory/theory.finger.html

substructure searching is known to be in the non-polynomial complete (NP-complete) class of computational problems.

we cant detect the presence of a substructure in polynomial time but we can often detect the absence of a substructure much faster often in linear time, an algorithm to detect the absence of a substructure (called a screen) with 100% confidence and presence with a lower confidence usually suffice in this case


type of screen for screening chemical databases

- structural keys - bitmaps where each bit represents the presence or absence of a specific structural feature (pattern)

 ```pattern & molecule```\
 a simple AND operation will indicate what structure in the pattern is present in the molecule (indicated by the bit position)

- fingerprints - unlike structural keys, fingerprints does not attribute any meaning to any particular bit
structural keys are usually very sparse. a fingerprint can be much smaller with the same discriminating power

\
variable-sized fingerprints

sparseness of a fingerprint is direcly related to its information density
folding a fingerprint to increase the information density

bit density is the ratio of "on" bits to the total number of bits

the folding process begins with a fixed fingerprint size that is large enough to accurately represent any molecule we expect to encouter. the fingerprint is then folded by dividing it into 2 equal halves then combine the 2 halves using a logical OR resulting into a shorter fingerprint with a higher bit density.\
fingerprint can be repeatedly folded until desired information density (called the min density) is reached or exceeded

fingerprint folding helps optimize the info density in a set of fingerprint, thus optimizing the screening speed.

\
Fingerprints and Reactions
- Structural reaction fingerprints
combination of the normal structural fingerprints for the reactant and product molecules within the reaction, which is the bitwise-OR of the following
	- fingerprint of the reactant part
	- fingerprint of the product part
	- bit-shifted fingerprint of the product part
agent molecules are not used in the structural fingerprint
srf provides discrimination power between reactant and product parts

- Reaction Difference fingerprints
for reaction processing
for a stoichiometric rnx (all atoms on the reactant side appear on the product side), diff in the fingerprints of the reactant and product will reflect the bond changes which occur during the rnx

the molecule fingerprints do not keep track of the count of paths so relevant bonds get masked out when we XOR between the reactant and product fingerprints, so we subtract the counts of each path in the reactant and product and set a bit in the difference fingerprint if non-zero, otherwise no bit is set for that path.

difference fingerprint may not be used as a substructure screen for any types of searching, but its useful as metric to track bond changes during reaction.

