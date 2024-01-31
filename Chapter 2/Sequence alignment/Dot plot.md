The dot plot, or dot matrix, is a technique of sequence alignment through visual inspection. We build a matrix with rows and columns equal to the length of the two sequences, and we put a sign where two characters are identical. Diagonal lines will then correspond to similarity regions.

## Interesting results
This type of plot can visually infer interesting results. The main diagonal line can be displaces in some points, resulting in 2 (or more) different lines that are separated by translation. This can be caused by insertions in only one of the two sequences. There can maybe be more then one parallel lines. This is probably caused by duplication in one of the two sequences. There can also be a palindrome section, caused by an inversion in one of the two sequences.

## Improving readability
**Filters** can be implemented in order to reduce strong background noise, present especially in nucleic acid sequences. To implement this filters we set a **stringency** value and a **window size**. We keep only the points in which for a given window size there are at least *stringency* points matching.

## Pros and cons
While with this method we can find all the possible matches while also finding repeated sequences (direct and inverse) and is useful for a quick inspection, the need for a manual visual inspection means that it cannot be fully automated, and is also affected by image compression if the sequence is too long. 


![[DotPlotExample.png]]![[DotPlot_real.png]]