# Carpe-DNA
## Central dogma
In  cellular DNA, genes are not actually contiguous but instead consist of disjoint coding segments called exons which are separated by noncoding introns. Transcription factors<sup>1</sup> recruit or block RNA polymerases at segments across the gene, resulting in a new splice of just the exons. The initiation and termination of transcription is determined by promoters and terminators respectively. Since genes are transcribed on demand instead of in advance, promoters can't be accessed sequentially and a mechanism is therefore needed to locate them.

All of this is important to know because we have a genetic algorithm that needs a granular way of imposing mutations for posterity. Loosely modeling on , the solution goes like this:
1. Represent DNA with a string of characters A, C, G, T. Our transcribe function, will take a promoter and terminator pair and locate the segment contained between them. The segment does not _not_ contain any other matching promoters or terminators.
2. The function is also given an intron which is removed from the transcription.
3. The Rabin-Karp algorithm is used as a subroutine to locate the promoter and terminator. 

> ### Rabin-Carp algorithm
 1. Compute rolling hash codes for query string *q* of length *n* and its target *t* of length *m*.
 2. Look at every character.
 3. Increment rolling hash for target string based on current character.
 4. If hash codes are equal, double check in the unlikely chance of collision by doing an exact comparison which has a Θ(n) runtime, which means the worse-case time-complexity could be O(nm). Therefore, the runtime is affected by how hash codes are generated. In the best case where the hash function has no collision, the time-complexity would be O(n+n).
>> #### Rolling hash function
1. A sliding window is analogous to reading from an online stream of data where there are performance benefits to element-wise strategies. An online hash function would 

---

<font size=1>

[1] Transcription factor, https://en.wikipedia.org/w/index.php?title=Transcription_factor&oldid=1208537646 (last visited Mar. 20, 2024).

</font>

