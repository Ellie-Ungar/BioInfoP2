



## Our Team

- Project Manager: **Torgeir Kjoeita**

Role: Torgeir coordinated the efforts of our group and lead us towards our final solution.
  
- Researcher: **Derek Parkinson**

Role: Derek provided background information regarding the algorithms we used to design our  solution. He enabled us to contextualize our work as well as completing the initial ground work necessary for us to begin building our solution.

- Quality Assurance Specialist: **Rick Djeuhon** 

Role: Rick tested our solution to make sure that it would function with a variety of test cases and analyzed our solution to make sure that it performed the necessary functions.

- Developer: **Carly Good**

- Developer: **Ali Yar Khan**

Role: Ali and Carly worked together to develop the DNA sequence matcher that took inputs from the user and outputted matching results.

- Technical Writer: **Ellie Ungar**

Role: Ellie curated and presented the work done by the group in this website, and created a presentation showcasing the solution.

- GUI Developer: **Seth Barker**

Role: Seth developed the GUI. As such, he was responsable for creating the user interface experience.



## History
The Smith-Waterman algorithm is a local algorithm that was proposed in 1981 by professors Temple F. Smith and Michael Waterman. Smith and Waterman intended to use dynamic programming for their algorithm and is based on its global opposite Needleman-Wunsch algorithm. Smith-Waterman was developed to calculate the local alignment of two given sequences and identifies similar DNA, RNA and protein segments. Smith-Waterman furthermore guarantees to find the optimal local alignment considering the given scoring system. The scoring system consists of a substitution matrix and a gap-scoring scheme. Scores include matches, mismatches, substitutions or insertions/deletions. Unlike in the Needleman-Wunsch algorithm, Smith-Waterman cannot display any negative scores in its scoring matrix and will set any of them to zero. The worst case in both time complexity and space complexity is O(mn), which is required to align two sequences of lengths m and n.

## Motivations
Because Smith-Waterman is a dynamic algorithm, it may be guaranteed to find the optimal local alignment, but it can also be computationally resource insensitive. It is also one of the slowest because of the number of computations required for the search. In order to speed up the algorithm, Single Instruction Multiple Data (SIMD) instructions have been used to parallelize the algorithm at the instruction level.

Smith Waterman does carry some disadvantages. An O(mn) complexity is very high for both time and space. This algorithm finds the alignment with maximal score, but not with maximal percent of matches. This algorithm tends to make ‘mosaics’ of well conserved fragments with connections by poorly-conserved fragments. A solution for that to perform length-normalized local alignment, which leads to the region with maximum degree of similarity.

Overall, our challenge was to create a piece of software that biologists can use to match DNA sequences from different people or different organisms.

## Analysis of Our Solution
The time complexity of our algorithms are as follows : 
Where;
N is the first/longest string
M is the second/shortest string

Divide and conquer is slow and inefficient. But it will return a correct solution. 
O(n^2)

Smith Waterman - O (n * m)
Runs slower than Greedy but faster than all other algorithms we have. It will also give a optimal output. When balancing speed and correctness Smith Waterman is the recommended solution. 

Brute force - always correct output. However it’s slow and during testing of long strings we would run out of memory.
O(n^2)

Greedy - Really fast but can and will give the wrong output. In our implementation it takes the first match it can finds and assumes that is the correct output. 
O(n * m)

![img](Img/graph.png)

## Test Files Illustrating Our Solution

Our Quality Assurance Specialist ran many tests to ensure that our solution was robust, and could handle a variety of inputs. The following is an example of such a test case, in which one input string being compared was a different length than the other:

Sample input:

Longer sequence compared to second sequence

seq1:ACCGTTCTGAGTCGATCACCGTTCTGAGTCGATC

seq2:ACCGTTCTGAGTCGATCACCGTTCT

---------------------------------------------

Input file : test 11.txt

Algorithm tested : ALL algorithms

Expected output : 25

Actual Output :25


For more from our Quality Assurance Specialist: all test files can be found here :<a href= "https://drive.google.com/open?id=1l4D3DFSI4ph1DigvAHtEv0Uj6f2quMfy" > in the google drive folder </a>

## How to Use our Program

Our program is straightforward and easy to use. Begin by running the GUI_Example class in your java IDE of choice. As soon as you hit "run", a small window, or GUI, should pop up for you to use. This GUI will except five inputs. The first three are your scoring weights. Use the drop down menu to add your desired scoring weights for a match, mismatch, and gap respectively. Next, use the final dropdown menu at the bottom left of the GUI to select with algorithm you'd like to run. You can chose between the Smith-Waterman Algorithm, the Brute Force Algorithm, the Greedy Algorithm, and the Divide and Conquer Algorithm. Finally, hit the "Choose File" button to select the file with your data. As soon as you select your file, the algorithm you have chosen will run, and you will see your outputs on the righthand side of the GUI.

## A Technical Explanation

#### The Smith-Waterman Algorithm:

    The Smith-Waterman algorithm performs its comparison by creating a matrix of scores for every possible subsequence of nucleotides   within the two sequences being compared. The code required to create this matrix is shown below. You can see where the user inputs are factored into the algorithm everywhere the variables "space", "match", and "mismatch" appear. At these locations in the code, the scoring values assigned to a match, mismatch, or space are used to calculate the score of the two substrings being compared.

		
		for (int i = 1; i <= x.length(); i++) {
			for (int j = 1; j <= y.length(); j++) {
				int score1 = scoreChart[i][j - 1] + space;
				int score2 = scoreChart[i - 1][j] + space;
				int score3 = 0;
				if (x.substring(i - 1, i).equalsIgnoreCase(y.substring(j - 1, j))) {
					score3 = scoreChart[i - 1][j - 1] + match;
				} else {
					score3 = scoreChart[i - 1][j - 1] + mismatch;
				}

				if (score1 > score2 && score1 > score3 && score1 > 0) {
					scoreChart[i][j] = score1;
				} else if (score2 > score3 && score2 > 0) {
					scoreChart[i][j] = score2;
				} else if (score3 > 0) {
					scoreChart[i][j] = score3;
				}

				if (scoreChart[i][j] > highestScore) {
					highestScore = scoreChart[i][j];
					Xco = i;
					Yco = j;
				}

			}
		}

Once the Smith-Waterman Algorithm has created this score matrix, it compares the scores at diagonal locations in the matrix in order to find the alignment that results in optimal scoring:

	boolean found = false;
		int i = Xco;
		int j = Yco;
		System.out.println(i + " " + scoreChart.length);
		System.out.println(j);

		while (!found) {
			if (scoreChart[i - 1][j - 1] > 0) {
				i--;
				j--;
			} else if (scoreChart[i - 1][j] > scoreChart[i][j - 1] && scoreChart[i - 1][j] > scoreChart[i][j]) {
				i--;
			} else if (scoreChart[i][j - 1] > scoreChart[i][j]) {
				j--;
			} else {
				found = true;
			}
		}

#### The Greedy Algorithm

We also implemented a much simpler scoring algorithm, known as the greedy algorithm. This algorithm simply increments the score for every mismatched nucleotide in the sequence, rather than finding an optimal alignment to ensure optimal scoring. As such, this algorithm is far less accurate than the Smith-Waterman Algorithm. Below, you can see how the scoring is incremented if nucleotides in position "i" on string A don't match the corresponding nucleotide in position "j" on string B:

	for (int j = 0; j < a.length() - 1; j++) {
				if (a.charAt(j) != b.charAt(j)) {
					score--;
				} else if (a.charAt(j) == b.charAt(j)) {
					score++;
			
				}
			}
		
		
#### The Brute Force Algorithm

The Brute Force Algorithm represents the most inefficient way to compare two nucleotide strings. Instead of efficiently comparing substrings of different lengths as in the Smith-Waterman algorithm, the Brute Force Algorithm compares all substrings of length one (the smallest possible length) one at a time. It then applies the scoring method to these substrings based on whether or not the substrings match or mismatch:

	if (a.substring(0, 1).equals(b.substring(0, 1))) {
					curScore += match;
				}
				
				
The Brute Force Algorithm deals with gaps by comparing the length difference between the two strings being compared:

	if (a.length() != b.length()) {
					curScore = Math.abs(a.length() - b.length()) * space;
				}

## Bibliography
[1] Norman Casagrande, Basic-Algorithms of Bioinformatics Applet, http://baba.sourceforge.net/, 2003.

[2] Freiburg RNA Tools. Teaching Smith-Waterman.

[3] Jacob Porter, Jonathan Berkhahn, Liqing Zhang. A Comparitive Analysis of Read Mapping and Indel Calling Pipelines for Next-Generation Sequencing Data.
In Emerging Trend in Computational Biology, Bioinformatics, and Systems Biology. 2015, pages 521-535.

[4] Supratim Choudhuri. Sequence Alignment and Similarity Searching in Genomic Databases.
In Bioinformatics for Beginners. 2014, pages 133-135.

[5] Julie Dawn Thompson. Heuristic Sequence Alignment Methods. 
In Statistics for Bioinformatics. 2016, pages 29-41.
