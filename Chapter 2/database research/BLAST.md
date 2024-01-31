Basic Local Alignment Search Tool is a program that searches for the best local alignment between the query sequence and all the database's sequences.
It's rapid, heuristic and works with alignments with gaps.
Wrt [[FASTA]] whereas FASTA searches for all possible words of the same length, BLAST limits the research to the most significant words using a *preventive* filter.
BLAST fixes the length of the word to 3 characters for proteins and 11 characters for nucleotides. It uses BLOSUM62 matrix to calculate the score.
BLAST has several phases:
- It generates a list of words of length W (3 or 11) from the query sequence (e.g. the sequence PQGAI will generate PQG-QGA-GAI). Then, for each word identified a list of all associated words is generated using BLOSUM62 substitution scores (e.g. considering PQG, one substitution could be with all characters substituting with themselves, obtaining a score of 18 according to BLOSUM62, but for example G could be substituted with E, obtaining a total score of 10 (P->P, Q->Q, G->E)) The associated words are total, so 20^3=8000 words. A score is associated with each word. A threshold is then used to reduce the number of words to the 50 most analogous (and repeated for each original 3 letter words obtained from the query sequence). For each query sequence the total number of words that will be used to search the database will be (for proteins) $50*(query\_len \ -2)$.
- After obtaining the most analogous words the program searches for the words in the database. The search is exact, since a screening of the words was already done previously.
- After finding the words in the database, an extension is performed. Basically the program tries to extend from both sides the words by comparing the query sequence and the found sequence (to which the word belongs). It does that until the extended alignment score start to decrease. This will produce alignments with higher score than the original one, which are called **High-scoring Segmented Pairs (HSP)**. The extension occurs 1 base at a time, but considers the two bases immediately adjacent to the found word. A HSP is considered relevant if it's score exceeds a threshold value called **S**. 
- At the end the best alignment using Smith-Waterman algorithm is returned for each HSP sequence that was selected (with score > then S)
In total we have 4 parameters: W,T,X,S. 
W is usually standard, 3 for proteins and 11 for nucleotides, and T is also usually standard (T is the threshold score for the 50 most analogous words), is set to 13 for proteins. S is usually set considering the expected value of a database with random sequences that would have >= score to S with the same length of the query sequence. Basically increasing S decreases this expected value and vice versa.

In particular we define E as equal to the number of sequences that we would expect to find if the database contained random sequences. E is thus influenced by the number of sequences in the database and the length of the query sequence. 
We also define the **p-value** as the probability of getting at random a value equal or higher than the obtained HSP as: $p=1-e^{-E}$. with E <0.01 p-value and E-value are very similar.
## Filters
BLAST has various filters to skip regions that present repetitions and low complexity:
- **SEG**: filters low protein complexity regions
- **DUST**: filters low DNA complexity regions
- **XNU**: filters regions containing tandem repetitions for proteins.
## BLAST versions 
- BLASTP: searches a protein sequence in a database of proteins.
- BLASTN: searches a nucleotide sequence in a database of nucleotide sequences.
- BLASTX: searches a nucleotide sequence translated in all six possible reading frames in a database of proteins.
- TBLASTN: searches a protein sequence in a database of nucleotide sequences that are automatically translated into all six possible reading frames.
- TBLASTX: searches translations in all six possible reading frames of a sequence of nucleotides in a database of nucleotide sequences dynamically translated.
## Other BLAST tools
- MegaBLAST: an optimized program to align nucleotide sequences that differ slightly and could be originated from sequencing errors.
- PSI-BLAST: aka Position Specific Iterated BLAST, it is designed for protein sequences analysis with an iterative procedure that increases sensitivity.
- BEAUTY (BLAST Enchanted Alignment UTilitY): adds information to the output of BLAST with text and graphics.
