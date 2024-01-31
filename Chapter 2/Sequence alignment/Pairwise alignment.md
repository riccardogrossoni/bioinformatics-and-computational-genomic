When comparing two sequences, there are 3 possible events that can occur:
- **Substitution**
- **Insertion**
- **Deletion**
Insertions and deletions are often called **indels**, since they are opposite. 
To discriminate between good and bad alignment we can define a scoring system that evaluate the use of substitutions and indels. This score can be used to evaluate either the distance between the 2 sequences or the [[similarity]].
There are two main ways to calculate the distance between two strings:
- **Hamming distance**: The number of mismatches between two strings of equal length.
- **Levenshtein distance (editing distance)**: the minimum number of operations to transform one string into the other.
## Formal definition 
In order to execute a pairwise alignment we must first set an **Alignment score** and we must define a **Scoring function**. We can then obtain the **Optimal alignment** by *maximizing* the similarity or *minimizing* the distance.
The scoring function can be created *ad-hoc*.
## Substitution matrices
Until now we have considered each type of substitution as the same, but is it really that way? For example, if we have an A nucleic acid, does it have the same odds of being substituted by any of the other bases or some base has an advantage compared to the others?
For this reasons we use **substitution matrices**. They assign a numerical value to each possible pair of characters that represents the probability of a nucleotide or amino acid of the pair to become the other, calculated in a certain evolutionary time. 
For [[Nucleotides]] the scoring is simple, but for amino acids ([[Proteins#Amino acids]]) their chemical differences must be accounted for. 
These matrices are symmetric, there are 2 main types:
- **PAM matrices (Percent/Point Accepted Mutations)**
- **BLOSUM matrices (BLOcks SUbstitution Matrices)**
## PAM matrices
For the construction of PAM matrices we first consider a set of closely related protein sequences as a reference, which must share a common ancestor. We then calculate the frequency of mutations between each pair of amino acid in the reference set to determine the probability of one amino acid changing into another. We then compute the log-odds ratios for each amino acid substitution (computing the logarithm of the ratio of the *observed probability* of a substitution to the *expected probability*). We then normalize the values. 
There are multiple PAM matrices available, identified with a number after the word PAM, for example PAM30 and PAM250; The number identifies the evolutionary distance, so we can choose the more appropriate matrix depending on the desired sensitivity to different degrees of sequence similarity. We can also obtain any PAMX matrix by simply taking the PAM1 matrix and elevating it to the X exponent.
## BLOSUM matrices
BLOSUM matrices are relatively similar to PAM matrices, but instead of being based on global alignments between sequences they are based on alignment of blocks of segments of amino acid sequences that are closely related. 
A block is defined as a highly conserved region without gaps. But to align the sequences the matrix of weights must be known. 
For each pair of amino acids *x* and *y* we want to calculate the **likelihood ($e_{xy}$)** that *x* and *y* are aligned by chance.
This calculus is based on the occurrences of x and y in the block, while also considering the times in which x and y are in the same column. 
$e_{xy}=p_xp_y/p_{xy}\ \ \ if \ \ \ x=y$  
$e_{xy}=2 \ p_xp_y/p_{xy}\ \ \ if \ \ \ x\neq y$  
$p_x$ and $p_y$ are the probabilities of x and y in the block (basically occurrence of x over total number of characters), while $p_{xy}$ is the probability of finding x and y paired in the same column. For the entry in the BLOSUM matrix we then calculate $-2log_2(e_{xy})$ and round to the nearest integer result to obtain the entry.
BLOSUM matrices available now have a number characterizing them that states that the sequences used in each cluster are similar to at least X% (with BLOSUM-X). The standard used is BLOSUM-62.
## Main differences
- PAM is based on an explicit evolutionary model, it observes mutation in global alignment, meaning that it includes both highly conserved regions and highly mutated ones.
- BLOSUM is based on implicit evolutionary model and only observes highly conserved regions in series of alignments without gaps.
BLOSUM with high numbers and PAM with low numbers are both designed for comparisons of closely related sequences. BLOSUM with low numbers and PAM with high numbers are designed for comparisons of distantly related proteins.
## Gaps
Gaps are an important topic for the alignment of sequences, since they are necessary for example to equalize the length of two sequences, but must be introduces only when strictly required, thus they must lower the alignment score. Also the score could change based on how much we are deleting, for example, should the deletion of 5 *consecutive* bases be counted as a penalty equal to 5 random bases deleted across the whole sequence length? Consecutive gaps are clearly more likely (instead of 1 single base "missing" a whole section is more probable). 
To handle this we make a distinction between gap **opening** and gap **extention**. Basically the first time we introduce a gap, the penalty is high, then if the extend that gap the penalty lowers.
## Computational techniques
The obvious method is to build all the alignments and find the best scoring one, but that obviously is way too expensive. There's a solution with dynamic programming, it requires to create a matrix \[n+1, m+1\] where n and m are the length of the 2 sequences and the +1 is added to account for gaps. We initialize the first cell with 0, then fill the first row and column with indel penalties. After this initialization we then fill each cell starting from the top left one following this procedure:
![[scoring_equation_in_alignment_matrix.png]]
Where *d* is the gap penalty, s(x,y) is the value in the substitution matrix and i,j refer to the position in the cells in the alignment matrix. We basically compare if going diagonally (direction down-right) has a higher value that proceeding from the left or from the top with a gap penalty.
The best score for the optimal alignment is obtained on the bottom right, and we can reconstruct the alignment by proceeding "backwards" until we reach the top left, aligning the two sequences that way. 
This way we obtain the following complexities:
- O(n + m) for initialization
- O(n * m) for calculation of elements
- O(n + m) for traceback
if n is circa m dimension-wise, then the total complexity is O(n^2), which is not low but a relatively decent result.
The algorithm for global alignment is called **Algorithm of Needleman-Wunsch** and a basic example is reported below.
Local alignment follows a similar structure to global alignment, but once the score goes below 0, then the cell is reset to zero. The algorithm, which is a derivation of Needleman-Wunsch, is called **Algorithm of Smith-Waterman**. The optimal local alignment is obtained starting from the cell with the highest value in the matrix, and the traceback is interrupted once a 0 is reached. As for global alignment an example is reported below.

## Example for global alignment
Sequence 1: ACTGGTCA
Sequence 2: ACCGTATC
GAP:            -2
MISMATCH: -1
MATCH:      +1
![[global_alignment_example.png]]

The resulting alignment has a score of -1 and the optimal alignment is the following:
```
A C C G T A T C -
A C T G G - T C A
```
   
This is not the only result, as we can see we could have gone diagonally after cell \[6,7] and then to the left instead of doing the opposite, resulting in the alignment:
```
A C C G T A T C -
A C T G - G T C A
```
## Example for local alignment
Sequence 1: ACCGGTCA
Sequence 2: ACCGTATC
GAP:            -2
MISMATCH: -1
MATCH:      +1
![[local_alignment_example.png]]
The resulting best alignment has a score of 4:
```
A C C G
A C C G
```
## Significance
There are 3 measures used to interpret the significance of a pairwise alignment:
- **Score Z**: after generating a large number of permutations of one of the 2 sequences we align each permutation with the other sequence and compute the score for each. We then calculate the difference between the original score and the mean of the obtained scores (of the permutations) and divide each for the standard deviation of the permutations. The resulting value, called Z, expresses the difference of the original correspondence from the random one (higher Z is better). Usually a score >5 suggests significance of the alignment between the 2 sequences
- **Probability p**: Expresses the probability of finding by chance a score equal or greater than some value S. $p=1-exp(-kmn* exp(- \lambda *S))$ with m the  query sequence, n the sequence found in the database, K and lambda some parameters dependent on the database and substitution matrix. There are various levels of p to determine the significance, but in general with p>10^-1 there is no correspondence (probably), while for p<10^-50 the two sequences are almost or completely equal. Values in between express a distant or close relationship depending on the value of p.
- **Value e**: Is the expected number of sequences in the database of random sequences with equal length of the query sequence that have a score greater or equal to the found sequence. if E is smaller then 10^-5 is generally a good alignment. 
