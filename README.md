# Gem5_Design_Space_Exploration
2nd lab for computer architecture


## Answers to questions


### _1. SPEC CPU2006 Benchmarks_

In file **config.ini**: <br/>

|cache     |  size |  assocciativity |
|----------|:------------:|-----------------:|
|L1 instruction cache (line: 789)| 32 KB | 2 |   
|L1 data cache (line: 155) | 64 KB | 2 |
|L2 cache (line: 994) | 2 MB | 8 |
|cache line size (line: 15) | 64 Bytes|  |

<br/>


|Benchmark     |  sim_seconds |  CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:------------:|:----:|:-----------------:|:-----------------:|:----------------:|
|specbzip | 0.087496 | 1.749911 | 0.000054 | 0.014624 | 0.266438 |  
|spechmmer| 0.058158 | 1.163153 | 0.000145  | 0.001669 | 0.081377 |
|speclibm | 0.174672 | 3.493438 | 0.000097 | 0.060971 | 0.999967 |
|speccmcf | 0.054421 | 1.088411 | 0.000019 | 0.001955 | 0.726153 |
|specsjeng| 0.513555 | 10.271094| 0.000015 | 0.121831 | 0.999979 |


---

### _2. Design Exploration_


---

### _3. Cost of efficiency and efficiency improvement_
