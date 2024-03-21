# Carpe DNA
## Background
In  cellular DNA, genes are not actually contiguous but instead consist of disjoint coding segments called exons which are themselves separated by noncoding introns. Transcription factors<sup>1</sup> recruit or block RNA polymerases at segments across the gene, resulting in a new splice of just the exons. The initiation and termination of transcription is determined by promoters and terminators respectively. Since genes are transcribed on demand instead of in advance, promoters can't be accessed sequentially and a mechanism is therefore needed to locate them.

All of this is important to know because we have a genetic algorithm that needs a granular way of imposing mutations for posterity. Loosely modeling on the rules of transcription, the solution goes like this:
1. Represent DNA with a string of characters A, C, G, T. Our transcribe function, will take a promoter and terminator pair and locate the segment contained between them. The segment does _not_ contain any other matching promoters or terminators.
2. The function is also given an intron which is removed from the transcription.
3. The Rabin-Karp algorithm is used as a subroutine to locate the promoter, terminator, and interon(s) before splicing a complete gene.

> ### Rabin-Carp algorithm
> 1. Compute rolling hash codes for query string *q* of length *n* with target *t* of length *m*.
> 2. Look at every character once.
> 3. Increment rolling hash for target string based on current character.
> 4. If hash codes are equal, confirm there wasn't a collision by doing an exact comparison (which has a Θ(n) runtime meaning the worst-case time-complexity could be up to O(nm)). Therefore, the runtime is affected by how hash codes are generated. In the best case where the hash function guarantees no collision, the time-complexity would be O(n+m).
>> #### Rolling hash function
>> A sliding window is analogous to reading from an online stream of data where there are performance benefits to using an element-wise strategy. An online hash function would not need the entire dataset to arrive at a solution by applying the transformation
$$\langle h_{i-n}, ...,h_{i-1}, \rangle\xRightarrow{H(c_i)} \langle h_{i-n+1}, ...,h_{i}, \rangle $$
where big *H* denotes the hashing function and little h denotes the element-wise solution for any character c. The hash function *H* is computed from the polynomial
$$H = c_1a^{k-1} + c_2a^{k-2} + \mathellipsis + c_ka^{0}$$
where query string of length *k* has characters *c<sub>i</sub>*

We naturally arrive at an object-oriented solution.

## Python implementation

```python
from dataclasses import dataclass
from functools import reduce
from math import inf
from random import choice, randrange

@dataclass
class Gene:
    promoter: str
    interon: str
    terminator: str

    @classmethod
    def randgene(cls):
        return cls(DNA.randseq(), DNA.randseq(), DNA.randseq())
    
class DNA:
    choices = list('ACGT')

    def __init__(self, seq):
        self.seq = seq
        
    def transcribe(self, gene):
        start = self.query(gene.promoter) + len(gene.promoter)
        end = self.query(gene.terminator, partition_start=start)

        # ---------++++++-------++++++-------++++++-----------
        # |        └exon0|      └exon1|      └exon2|
        # └promoter  /   └interon /   └interon  /  └terminator
        #           /            /             /
        #           └—>combine<–>└<–>combine<––└
        #           |===========RNA============|
        exons = []  
        curr_interon = start + len(gene.promoter)
        while True:
            next_interon = self.query(gene.interon, 
                                      partition_start = curr_interon + len(gene.interon),
                                       partition_end=end)
            print(next_interon)
            if next_interon == -1 or next_interon >= end:
                break
            exons.append(self.seq[curr_interon:next_interon])
            curr_interon = next_interon
        return ''.join(exons)

    def query(self, pattern, partition_start=0, partition_end=inf):
        BASE = len(self.choices)
        pattern_hash = reduce(lambda h,c: h * BASE + self.choices.index(c), 
                              pattern, 0)
        target_hash = reduce(lambda h,c: h * BASE + self.choices.index(c), 
                             dna.seq[:len(pattern)], 0)
        pattern_power = BASE**max(len(pattern) - 1, 0)
        for i in range(len(pattern), len(dna.seq)+1):
            if ((pattern_hash == target_hash or i == len(dna.seq)) and 
                dna.seq[i-len(pattern):i]): 
                return i - len(pattern)
            newest, oldest = dna.seq[i], dna.seq[i-len(pattern)] 
            target_hash -= self.choices.index(oldest) * pattern_power
            target_hash = target_hash * BASE + self.choices.index(newest)
        return -1
    
    @staticmethod
    def randseq(start=1, end=5, codons=True):
        return ''.join([choice(DNA.choices) 
                for _ in range((3 if codons else 1) ** randrange(start, 
                                                                 end))])
    
    @classmethod
    def randDNA(cls, gene):
        dna_seq =  (DNA.randseq() + gene.promoter +
                    f'ATG{gene.interon}CGA{gene.interon}TCGGACAGTCGA'
                    f'{gene.interon}GTCCAG{gene.interon}TAGACGATC' +
                    gene.terminator + DNA.randseq())
        total_exons = randrange(1,10)
        
        prefix = ''.join([DNA.randseq(), gene.promoter])
        dna_gene = ''.join(
            [DNA.randseq() + gene.interon for _ in range(total_exons)] + 
            [DNA.randseq()]
        )
        suffix = ''.join([DNA.randseq(), gene.terminator, DNA.randseq()])
        return cls(''.join([prefix, dna_gene, suffix]))
if __name__ == '__main__':
    gene = Gene.randgene()
    dna = DNA.randDNA(gene)
    print(dna.transcribe(gene))
```

## Expectations
Superficially, the issue is with **DNA::transcribe** which never terminates. Here, the Rabin-Karp subroutine **DNA::query** is used to locate the gene boundaries and then assemble the indices for exons before finally constructing a new string. The following help is needed:
* Identify the root cause(s) of our infinite while-loop. 
* Provide a working version along with an explanation of what was fixed.
* Supply evidence that the provided version works by
 * showing the output of running `print(dna.transcribe(gene))`,
 * constructing non-random **Gene** and **DNA** instances with assert statements that verify the actual and expected transcription.

---

<font size=1>

[1] Transcription factor, https://en.wikipedia.org/w/index.php?title=Transcription_factor&oldid=1208537646 (last visited Mar. 20, 2024).

</font>

