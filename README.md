



## Our Team

- Project Manager: **Torgeir Kjoeita**

- Researcher: **Derek Parkinson**

- Quality Assurance Specialist: **Rick Djeuhon** 

- Developer: **Carly Good**

- Developer: **Ali Yar Khan**

- Technical Writer: **Ellie Ungar**

- GUI Developer: **Seth Barker** 



## History and Background
The Smith-Waterman algorithm is a local algorithm that was proposed in 1981 by professors Temple F. Smith and Michael Waterman. Smith and Waterman intended to use dynamic programming for their algorithm and is based on its global opposite Needleman-Wunsch algorithm. Smith-Waterman was developed to calculate the local alignment of two given sequences and identifies similar DNA, RNA and protein segments. Smith-Waterman furthermore guarantees to find the optimal local alignment considering the given scoring system. The scoring system consists of a substitution matrix and a gap-scoring scheme. Scores include matches, mismatches, substitutions or insertions/deletions. Unlike in the Needleman-Wunsch algorithm, Smith-Waterman cannot display any negative scores in its scoring matrix and will set any of them to zero. The worst case in both time complexity and space complexity is O(mn), which is required to align two sequences of lengths m and n.

## Motivations and Problem Statments
Because Smith-Waterman is a dynamic algorithm, it may be guaranteed to find the optimal local alignment, but it can also be computationally resource insensitive. It is also one of the slowest because of the number of computations required for the search. In order to speed up the algorithm, Single Instruction Multiple Data (SIMD) instructions have been used to parallelize the algorithm at the instruction level.

Smith Waterman does carry some disadvantages. An O(mn) complexity is very high for both time and space. This algorithm finds the alignment with maximal score, but not with maximal percent of matches. This algorithm tends to make ‘mosaics’ of well conserved fragments with connections by poorly-conserved fragments. A solution for that to perform length-normalized local alignment, which leads to the region with maximum degree of similarity.


## Analysis of Our Solution

## Test Files Illustrating Our Solution

## How to Implement Our Solution

## A Technical Explanation

## Bibliography


