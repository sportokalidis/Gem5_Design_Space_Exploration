# Gem5_Design_Space_Exploration
2nd lab for computer architecture


## Answers to questions


### _1. SPEC CPU2006 Benchmarks_
## 1
In file **config.ini**: <br/>

|cache     |  size |  assocciativity |
|----------|:------------:|:-----------------:|
|L1 instruction cache (line: 789)| 32 KB | 2 |   
|L1 data cache (line: 155) | 64 KB | 2 |
|L2 cache (line: 994) | 2 MB | 8 |
|cache line size (line: 15) | 64 Bytes|  |

<br/>

## 2
|Benchmark     |  sim_seconds |  CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:------------:|:----:|:-----------------:|:-----------------:|:----------------:|
|specbzip      | 0.087496 | 1.749911 | 0.000054 | 0.014624 | 0.266438 |  
|spechmmer     | 0.058158 | 1.163153 | 0.000145 | 0.001669 | 0.081377 |
|speclibm      | 0.174672 | 3.493438 | 0.000097 | 0.060971 | 0.999967 |
|speccmcf      | 0.054421 | 1.088411 | 0.000019 | 0.001955 | 0.726153 |
|specsjeng     | 0.513555 | 10.271094| 0.000015 | 0.121831 | 0.999979 |

<br/>

## 3
|parameter                   |  --cpu-clock=2GHZ (default) | --cpu-clock=1GHz |
|----------------------------|:---------------------------:|:----------------:|
|system.clk_domain.clock     |           1000              |        1000      |   
|system.cpu_clk_domain.clock |            500              |        1000      |

<br/>

---

### _2. Design Exploration_

In this part of exercise , we will try to choose the suitable parameters in order to succeed a better performance for our system, for each benchmark: <br/>

***Average memory access time = Hit time + Miss rate × Miss penalty*** <br/>

**Reducing the miss rate**: larger block size, larger cache size, and higher associativity.
**Reducing the miss penalty**: multilevel caches.


The classical approach to improving cache behavior is to reduce miss rates. To gain better insights into the causes of misses, we first start with a model that sorts all misses into three simple categories:<br/><br/>

**Compulsory misses**: The very first access to a block cannot be in the cache, so the
block must be brought into the cache. These are also called cold-start misses
or first-reference misses.<br/>
**Capacity misses**: If the cache cannot contain all the blocks needed during execution
of a program, capacity misses (in addition to compulsory misses) will occur
because of blocks being discarded and later retrieved.<br/>
**Conflict misses**: If the block placement strategy is set associative or direct mapped,
conflict misses (in addition to compulsory and capacity misses) will occur
because a block may be discarded and later retrieved if too many blocks map
to its set. These misses are also called collision misses. The idea is that hits in
a fully associative cache that become misses in an n-way set-associative
cache are due to more than n requests on some popular sets.<br/>

* **Increase Block size**
  + Reduces compulsory misses
  + Increases capacity and conflict misses, increases miss penalty

* **Increase capacity of the cache**
  + Increases hit time, increases power consumption

* **Higher associativity**
  + Reduces conflict misses
  + Increases hit time, increases power consumption

* **Higher number of cache levels**
  + Reduces overall memory access time

<br/>

#### specbzip optimization

|file  | L1 icache size| L1 dcache size | L2 cache size|L1 icache assoc|L1 dcache assoc|L2 cache assoc|cache line size|
|:----:|:-------------:|:--------------:|:------------:|:-------------:|:-------------:|:------------:|:-------------:|
|file 1|32 KB          |128 KB          |2 MB          |1              |1              |8             |128 Bytes      |
|file 2|32 KB          |128 KB          |2 MB          |2              |2              |8             |128 Bytes      |
|file 3|32 KB          |64 KB           |4 MB          |2              |2              |8             |128 Bytes      |
|file 4|32 KB          |64 KB           |2 MB          |2              |2              |8             |128 Bytes      |
|file 5|128 KB         |128 KB          |4 MB          |4              |2              |8             |128 Bytes      |

<br/>

|file          | CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:----:|:----------------:|:----------------:|:---------------:|
|file 1        | 1.726321| 0.013390| 0.000052| 0.172283| 
|file 2        | 1.694440| 0.010690| 0.000044| 0.217145| 
|file 3        | 1.672496| 0.010683| 0.000044| 0.187883| 
|file 4        | 1.552696| 0.009989| 0.000070| 0.383919| 
|file 5        | 1.546647| 0.008772| 0.000052| 0.259662| 

#### spechmmer optimisation

|file  | L1 icache size| L1 dcache size | L2 cache size|L1 icache assoc|L1 dcache assoc|L2 cache assoc|cache line size|
|:----:|:-------------:|:--------------:|:------------:|:-------------:|:-------------:|:------------:|:-------------:|
|file 1|32 KB          |128 KB          |2 MB          |1              |1              |8             |128 Bytes      |
|file 2|32 KB          |128 KB          |2 MB          |2              |2              |8             |128 Bytes      |
|file 3|32 KB          |64 KB           |4 MB          |2              |2              |8             |128 Bytes      |
|file 4|32 KB          |64 KB           |2 MB          |2              |2              |8             |128 Bytes      |
|file 5|128 KB         |128 KB          |4 MB          |4              |2              |8             |128 Bytes      |

<br/>

|file          |CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:----:|:----------------:|:----------------:|:---------------:|
|file 1        | 1.160014|0.000904|0.000061|	0.085634|
|file 2        | 1.159969|0.000904|0.000053|  0.085931| 
|file 3        | 1.167442|0.000420|0.000141|       -  |
|file 4        | 1.177802|0.000300|0.000056|	0.251618|
|file 5        | 1.177802|0.000300|0.000056|	0.251618|


#### speclibm optimisation

|file  | L1 icache size| L1 dcache size | L2 cache size|L1 icache assoc|L1 dcache assoc|L2 cache assoc|cache line size|
|:----:|:-------------:|:--------------:|:------------:|:-------------:|:-------------:|:------------:|:-------------:|
|file 1|64 KB          |32 KB           |4 MB          |1              |1              |8             |128 Bytes      |
|file 2|64 KB          |64 KB           |-             |2              |2              |-             |128 Bytes      |
|file 3|32 KB          |64 KB           |-             |2              |2              |-             |128 Bytes      |
|file 4|128 KB         |128 KB          |2 MB          |1              |4              |1             |256 Bytes      |
|file 5|128 KB         |128 KB          |4 MB          |2              |2              |1             |256 Bytes      |
|file 6|32 KB          |64 KB           |2 MB          |4              |2              |1             |256 Bytes      |
|file 7|128 KB         |128 KB          |-             |2              |2              |-             |256 Bytes      |

<br/>

|file          |  CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:----:|:----------------:|:----------------:|:---------------:|
|file 1        | 2.616087|0.033071|	0.000107|	0.895066| 
|file 2        | 2.166548|0.030486| 0.000097|	-       |
|file 3        | 2.166617|0.030486|	0.000105|	-       |
|file 4        | 1.654711|0.015244|	0.000095|	0.999804|
|file 5        | 1.654698|0.015244|	0.000082|	0.999909|
|file 6        | 1.654698|0.015244| 0.000081|	0.999917|
|file 7        | 1.524595|0.015244|0.000079 | 	-     |


#### specmcf optimisation

|file  | L1 icache size| L1 dcache size | L2 cache size|L1 icache assoc|L1 dcache assoc|L2 cache assoc|cache line size|
|:----:|:-------------:|:--------------:|:------------:|:-------------:|:-------------:|:------------:|:-------------:|
|file 1|32 KB          |128 KB          |2 MB          |1              |1              |8             |128 Bytes      |
|file 2|32 KB          |128 KB          |-             |2              |2              |-             |64 Bytes       |
|file 3|128 KB         |128 KB          |4 MB          |2              |2              |8             |128 Bytes      |
|file 4|128 KB         |128 KB          |2 MB          |2              |2              |8             |128 Bytes      |
|file 5|128 KB         |128 KB          |4 MB          |4              |2              |8             |128 Bytes      |

<br/>

|file          |  CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:----:|:----------------:|:----------------:|:---------------:|
|file 1        |  1.187895|	0.003301|	0.015123|	0.081385|
|file 2        |  1.288342|	0.002203|	0.015212|	NAN |
|file 3        |  1.113684|	0.001120|	0.000013|	0.739937|
|file 4        |  1.111121|	0.001104|	0.000013|	0.660414|
|file 5        |  1.117051|	0.001104|0.000013 |	0.868933|


#### specsjeng optimisation

|file  | L1 icache size| L1 dcache size | L2 cache size|L1 icache assoc|L1 dcache assoc|L2 cache assoc|cache line size|
|:----:|:-------------:|:--------------:|:------------:|:-------------:|:-------------:|:------------:|:-------------:|
|file 1|32 KB          |128 KB          |-             |2              |2              |-             |64 Bytes      |
|file 2|64 KB          |32 KB           |4 MB          |1              |1              |8             |128 Bytes      |
|file 3|64 KB          |64 KB           |-             |2              |2              |-             |128 Bytes      |
|file 4|32 KB          |128 KB          |-             |2              |2              |-             |128 Bytes      |
|file 5|32 KB          |64 KB           |512 kB        |2              |2              |1             |128 Bytes      |
|file 6|32 KB          |64 KB           |-             |2              |2              |-             |128 Bytes      |
|file 7|128 KB         |128 KB          |4 MB          |4              |2              |-             |128 Bytes      |
|file 8|64 KB          |64 KB           |512 KB        |4              |2              |1             |128 Bytes      |
|file 9|128 KB         |128 KB          |-             |4              |2              |-             |128 Bytes      |


<br/>

|file          |  CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:----:|:----------------:|:----------------:|:---------------:|
|file 1        |8.062464|	0.121854|	0.000016|	- |
|file 2        |6.797811|	0.061073|	0.000013|	0.994937 | 
|file 3        |5.573538|	0.060918|	0.000013|	-  |
|file 4        |5.736775|	0.060918|	0.000014|	-  |
|file 5        |6.801393|	0.060918|	0.000014|	0.999956 | 
|file 6        |5.736561|	0.060918|	0.000014|	-  |
|file 7        |4.972486|	0.060918|	0.000013|	0.999978|
|file 8        |4.976551|	0.060918|	0.000013|	0.999974|
|file 9        |3.840362|	0.060917|	0.000012|	-  |


---

### _3. Cost of efficiency and efficiency improvement_
