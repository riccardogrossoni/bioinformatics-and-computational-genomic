Given 2 sequences we are interested in:
- the degree of [[Similarity]];
- the **correspondence** between elements of the sequences;
- the observation of patterns of conservation and variability;
- the evolutionary relationship;
The comparison between sequences allow us to predict the structure (e.g. 2 amino acid that have 20-30% of the same residues aligned can have a very similar 3D structure) which can give further hints on the function of that structure, but sequence comparison can also be used for a **phylogenetic analysis** to infer information about evolution.

## Criteria
The main way to infer a conclusion on the comparison of two sequences is [[Homology]]. Amino acidic sequences are homologous if they share 25% of the amino acids aligned and Nucleotide sequences are homologous if they share 70% of the nucleotides aligned.
Another important criteria is Similarity, that is an observable quantity expressed as a percentage. There are 3 main search types:
- We define **Homology search** as the act of searching a given sequence called **query** among known sequences which are used, if homolog, to interpret the new sequence.
- We define **Motive search** as the act of searching known sets of characters (called **motive**) for which we know the functions, inside new sequences, to infer possible functions of such sequence. Often this type of search is not feasible and homology based searches are preferable.
- We define **Similarity search** as the act of identifying unknown sequences, to find other members of family of genes and proteins, to find relationships between proteins, to find regions that are conserved through evolution etc.

## Sequence alignment
First of all in order to compare sequences we must first align them. There are two main ways of aligning two or more sequences:
- **Global alignment**
- **Local alignment**
There are various methods that compare sequences that will be analyzed in separate files, here the recap.

## Global and local alignment
- **[[Dot plot]]**
- **[[Pairwise alignment]]**, in particular **[[Pairwise alignment#PAM matrices]]** and **[[Pairwise alignment#BLOSUM matrices]]**
## Database research
Until now we have evaluated the alignment and comparison of 2 sequences, but usually we want to compare a new sequence with a database of known ones. 
There are already programs considered "classic" that specialize in that function:
- **[[FASTA]]**
- **[[BLAST]]**
The principle for both of them is to search for "words" in the database, which is a short series of characters in the sequences of either amino acids or nucleotides.
The words are indicated with a k-tuple term, where k is the number of characters.
This method is based on the hypothesis that related sequences share many words.
The 2 most important values for database research are:
- [[Sensitivity]]
- [[Specificity]]
In general long words lead to increased specificity and reduced [[Sensitivity]]. A compromise between the two must always be made during database research.

But which is best? Here a brief confrontation for the two programs:
- BLAST is the standard tool used in practice, is more sensitive to protein research, uses local alignment and is fast.
- FASTA is more sensitive, especially for nucleotide sequences, uses global alignment and is slower, since the answers arrive to the user through email.
Both are heuristic, they are optimized to find most of the matches, sacrificing sensitivity to gain velocity. For this reason they are not guaranteed to find the best alignment between two sequences.

## Multiple alignment
Until now we have seen [[pairwise alignment]] (each time we aligned 2 sequences), but with multiple alignment we can work on molecular phylogeny and construct phylogenic trees that illustrate distances and evolutionary relationships among analyzed molecules. It can also be used to study evolution of [[genome]] and identify recurring motifs or functionally important sites.

## Definition of multiple alignment
A global alignment of a set of sequences is obtained through the introduction of gaps. Obviously there should not be a column with only gaps. At the end of the operation all the Sequences with gaps introduced must have equal length.
One of the useful things that can be done is to color-code for example the nucleotides or the amino acids based on some characteristics.
We can the build **Profiles** which are useful structures for summarizing the common proprieties of groups of sequences and are the basis of many methods of multiple sequence alignment. A profile is a matrix of dimensions equal to the length of the sequences after adding gaps times the total number of possible characters characters +1 (for example, if we have a set of nucleotide sequences that after adding gaps have length 10, then the matrix will be of dimension 10 x 4+1). Each column represents a position in the alignment and each cell represents the frequency of the row's character in that position. The profile matrix is also known as **Position Specific Scoring Matrix (PSSM)**.
While elaborating on the profiles let's remind the definition of [[Shannon Entropy]] and [[Information content]].
From the profile matrix we can extract the **logo** which shows graphically the information content of each position of the multiple alignment.
![[logo_profile_matrix.png]]
As we can see from the example, the height of the letters are proportional of how much the letter is preserved in the sequences, so this can be a good indication of the conservation of that base in that particular stretch.

How is the alignment done? To align a sequence to a profile we use the Needleman-Wunsch algorithm with an appropriate scoring function that is defined from the profile itself.
We can also edit the scoring function to be able to align 2 different profiles.

What do we use as scoring function? The most used is the **Sum of Pairs algorithm**, that states that the multiple alignment score is the sum of all single alignment scores (basically we do a pair alignment for each pair of sequences, then sum all the scores obtained).
This is not the only scoring function available, other widely used are **Entropy scoring function** and **Circular sum scoring function**. The choice of the right scoring function is crucial and unfortunately there is no universal scoring function available.

## Dynamic programming for multiple alignment problem
To align n sequences we can use a n-dimensional hypercube by defining $D(j_1, j_2, j_3,... j_n)$ as the best score of the alignment of prefixes of length $j_1, j_2, j_3, ..., j_n$ of the sequences x1 through xn. We obviously initialize D(0,0,...,0)=0 and then expand the 2-dimensional algorithm (can be found in [[Pairwise alignment#Computational techniques]]) to be n-dimensional (following the same structure of "diagonal" and lateral blocks, but of course in n-dimensions).
![[3D_alignment.png]]
Here an example in 3D, any higher dimension cannot be visualized.
In practice, this is not feasible. let's make an example: you have 10 sequences, of length l=100, the matrix will be an hypercube with $100^{10}$ elements, requiring 100 million terabytes of space. This is obviously ridiculous and unfeasible.
Optimal multiple alignment cannot be solved in polynomial time, so we have to use heuristics and approximations.
We have multiple options:
- **Progressive alignment**
- **Center-star alignment**
- **Iterative alignment**
- **Alignment through Hidden Markov Models**
- **Alignment through Fast Fourier Transform**
The most common method is progressive alignment, that is based on the construction of a series of pairwise alignments. The strategy is to align the two most similar sequences at first, then align the next 2 best ones and so on until all the sequences are aligned pairwise, then merge them with alignments of profiles until the end.
![[Progressive_alignment.png]]