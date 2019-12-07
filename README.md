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


|file          | CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:----:|:----------------:|:----------------:|:---------------:|
|file 1        | 1.726321| .013390| .000052| .172283| 
|file 2        | 1.694440| .010690| .000044| .217145| 
|file 3        | 1.672496| .010683| .000044| .187883| 
|file 4        | 1.552696| .009989| .000070| .383919| 
|file 5        | 1.546647| .008772| .000052| .259662| 

#### spechmmer optimisation

|file          |CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:----:|:----------------:|:----------------:|:---------------:|
|file 1        | 1.160014|0.000904|0.000061|	0.085634|
|file 2        | 1.159969|0.000904|0.000053|  0.085931| 
|file 3        | 1.167442|0.000420|0.000141|       -  |
|file 4        | 1.167442|0.000420|0.000141|       -  |
|file 5        | 1.160217|0.000904|0.000141|	0.082767|


#### speclibm optimisation

|file          |  sim_seconds |  CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:------------:|:----:|:----------------:|:----------------:|:---------------:|
|file 1        |  |
|file 2        |  |
|file 3        |  |
|file 4        |  |
|file 5        |  |


#### speccmcf optimisation

|file          |  sim_seconds |  CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:------------:|:----:|:----------------:|:----------------:|:---------------:|
|file 1        |  |
|file 2        |  |
|file 3        |  |
|file 4        |  |
|file 5        |  |


#### specsjeng optimisation

|file          |  sim_seconds |  CPI | L1 icache misrate| L1 dcache misrate| L2 cache misrate|
|--------------|:------------:|:----:|:----------------:|:----------------:|:---------------:|
|file 1        |  |
|file 2        |  |
|file 3        |  |
|file 4        |  |
|file 5        |  |


---

### _3. Cost of efficiency and efficiency improvement_
