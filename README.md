# Independent replication of the performance experiments of Matjuice from Vincent Foley-Bourgon's Master Thesis

The performance results obtained on a less powerful machine, the 2011 Macbook Air model, are congruent with the results published in the Master Thesis and the DLS paper. The benchmarks on which the code produced by Matjuice is slowest (clos, fdtd) are slower by an additional factor or 2-4x. The exact cause will be investigated.

Notes regarding the benchmark implementations used:

* The babai algorithm expects a triangular matrix but triu() is not supported by Matjuice. The results were obtained by removing the triu() call and using directly the matrix of random values. Moreover, randn() in Matjuice does not return numbers according to the normal distribution. It returns numbers according to the uniform distribution (it returns the same numbers as rand()). Although the result computed is not meaningful it seems the number of operations performed is the same, therefore the performance result should not be affected. This will be confirmed once triu() and randn() are implemented in Matjuice. To run the benchmark with Matjuice you therefore need to modify the current implementation to remove the triu() call and remove the output to deactivate the correctness check; 
* Also regarding the babai matlab implementation: when it is executed on Mathworks' MATLAB environment with the medium size (used for the performance evaluation) the output vector is composed of NaN results. This is not the case for the small input size. The input should therefore be conditioned to return something meaningful, otherwise I am not sure whether the performance results are meaningful for the MATLAB implementation;
* The fdtd algorithm 
* fft
* dich

Additional notes: All the benchmarks used in the thesis, which were part of the Ostrich2 suite, were each migrated to their own independent repository to take advantage of Wu-Wei automatic installation capabilities. This will ease the replication of some specific results without having to rerun all the tests. It will be used to improve the performance of the generated code on the slowest benchmarks.


### Invariants (configuration parameters that are the same for all runs) ###


| category       | short-name |
| -------------- | ---------- |
| implementation | matlab     |
| platform       | mba-2011   |
| input-size     | medium     |

Platform:

    {
    	"type": "platform",
    	"short-name": "mba-2011",
    	"name": "Darwin-15.6.0-x86_64-i386-64bit",
    	"cpu": "Intel Core i7",
    	"gpu": "Intel HD Graphics 3000",
    	"memory": "4 GB",
    	"os": "Mac OS X 10.11.6",
    	"supported-languages": ["x86_64"],
    	"supported-formats": ["binary"],
    	"environments": []
    }

### Results ###

| benchmark  | compiler      | environment | mean      | std      | min       | max       | repetitions |
| ---------- | ------------- | ----------- | --------- | -------- | --------- | --------- | ----------- |
| babai      | matjuice      | chrome      | 1.6938s   | +-4.21%  | 1.5520s   | 1.7700s   | 10          |
| babai      | matjuice      | firefox     | 1.4152s   | +-14.92% | 1.1320s   | 1.6880s   | 10          |
| babai      | matjuice      | node        | 1.7285s   | +-3.57%  | 1.6440s   | 1.8600s   | 10          |
| babai      | matlab-concat | matlab-vm   | 0.2139s   | +-11.29% | 0.1918s   | 0.2760s   | 10          |
| bubble     | matjuice      | chrome      | 0.6421s   | +-1.65%  | 0.6220s   | 0.6550s   | 10          |
| bubble     | matjuice      | firefox     | 0.5868s   | +-11.79% | 0.5220s   | 0.7230s   | 10          |
| bubble     | matjuice      | node        | 0.6432s   | +-5.56%  | 0.5970s   | 0.7320s   | 10          |
| bubble     | matlab-concat | matlab-vm   | 2.2209s   | +-2.94%  | 2.0907s   | 2.3407s   | 10          |
| capr       | matjuice      | chrome      | 1.0173s   | +-5.19%  | 0.9430s   | 1.1200s   | 10          |
| capr       | matjuice      | firefox     | 1.9551s   | +-9.77%  | 1.6670s   | 2.3880s   | 10          |
| capr       | matjuice      | node        | 0.9743s   | +-5.27%  | 0.9250s   | 1.0920s   | 10          |
| capr       | matlab-concat | matlab-vm   | 3.3679s   | +-7.12%  | 3.1702s   | 3.8406s   | 10          |
| clos       | matjuice      | chrome      | 118.6106s | +-2.21%  | 114.6550s | 122.0900s | 10          |
| clos       | matjuice      | firefox     | 123.2713s | +-4.14%  | 120.1530s | 129.1640s | 3           |
| clos       | matjuice      | node        | 107.6356s | +-7.00%  | 93.1660s  | 116.0470s | 10          |
| clos       | matlab-concat | matlab-vm   | 0.3360s   | +-10.90% | 0.3093s   | 0.4153s   | 10          |
| collatz    | matjuice      | chrome      | 1.6259s   | +-4.36%  | 1.5760s   | 1.8190s   | 10          |
| collatz    | matjuice      | firefox     | 1.6610s   | +-3.71%  | 1.5810s   | 1.7650s   | 10          |
| collatz    | matjuice      | node        | 4.5354s   | +-19.97% | 3.9580s   | 7.0310s   | 10          |
| collatz    | matlab-concat | matlab-vm   | 11.3342s  | +-4.59%  | 11.0415s  | 12.7897s  | 10          |
| crni       | matjuice      | chrome      | 16.2237s  | +-27.63% | 13.2480s  | 24.7470s  | 10          |
| crni       | matjuice      | firefox     | 17.2653s  | +-4.73%  | 15.8440s  | 18.4470s  | 10          |
| crni       | matjuice      | node        | 14.2550s  | +-9.76%  | 12.6680s  | 16.8170s  | 10          |
| crni       | matlab-concat | matlab-vm   | 3.4699s   | +-3.59%  | 3.3578s   | 3.7667s   | 10          |
| dich       | matjuice      | chrome      | 0.4777s   | +-2.81%  | 0.4570s   | 0.4990s   | 10          |
| dich       | matjuice      | firefox     | 0.4531s   | +-11.39% | 0.4030s   | 0.5910s   | 10          |
| dich       | matjuice      | node        | 1.0186s   | +-1.91%  | 0.9880s   | 1.0410s   | 10          |
| dich       | matlab-concat | matlab-vm   | 2.1829s   | +-3.71%  | 2.0638s   | 2.3535s   | 10          |
| fdtd       | matjuice      | chrome      | 201.4680s | +-84.05% | 96.4670s  | 396.8260s | 3           |
| fdtd       | matjuice      | firefox     | 62.7893s  | +-5.97%  | 58.8120s  | 66.2610s  | 3           |
| fdtd       | matjuice      | node        | 128.3907s | +-2.39%  | 126.2500s | 131.9030s | 3           |
| fdtd       | matlab-concat | matlab-vm   | 0.3358s   | +-4.80%  | 0.3205s   | 0.3526s   | 3           |
| fft        | matjuice      | chrome      | 0.4502s   | +-7.38%  | 0.4060s   | 0.4930s   | 10          |
| fft        | matjuice      | firefox     | 0.7531s   | +-10.77% | 0.6260s   | 0.8700s   | 10          |
| fft        | matjuice      | node        | 0.4064s   | +-3.67%  | 0.3920s   | 0.4390s   | 10          |
| fft        | matlab-concat | matlab-vm   | 1.4333s   | +-12.89% | 1.3068s   | 1.8973s   | 10          |
| fiff       | matjuice      | chrome      | 0.9367s   | +-16.04% | 0.7210s   | 1.0770s   | 10          |
| fiff       | matjuice      | firefox     | 1.3444s   | +-11.34% | 1.1110s   | 1.5780s   | 10          |
| fiff       | matjuice      | node        | 0.8719s   | +-35.74% | 0.7160s   | 1.7290s   | 10          |
| fiff       | matlab-concat | matlab-vm   | 3.2412s   | +-2.16%  | 3.1622s   | 3.3412s   | 10          |
| lgdr       | matjuice      | chrome      | 0.4304s   | +-6.54%  | 0.3940s   | 0.4850s   | 10          |
| lgdr       | matjuice      | firefox     | 0.6059s   | +-7.12%  | 0.5530s   | 0.6720s   | 10          |
| lgdr       | matjuice      | node        | 0.8724s   | +-4.80%  | 0.8330s   | 0.9790s   | 10          |
| lgdr       | matlab-concat | matlab-vm   | 0.2595s   | +-5.15%  | 0.2415s   | 0.2781s   | 10          |
| makechange | matjuice      | chrome      | 0.1504s   | +-7.95%  | 0.1310s   | 0.1770s   | 10          |
| makechange | matjuice      | firefox     | 0.2996s   | +-55.30% | 0.1270s   | 0.5300s   | 10          |
| makechange | matjuice      | node        | 0.1411s   | +-7.70%  | 0.1290s   | 0.1660s   | 10          |
| makechange | matlab-concat | matlab-vm   | 0.5553s   | +-6.37%  | 0.5355s   | 0.6537s   | 10          |
| matmul     | matjuice      | chrome      | 0.1685s   | +-4.71%  | 0.1580s   | 0.1860s   | 10          |
| matmul     | matjuice      | firefox     | 0.1808s   | +-6.21%  | 0.1670s   | 0.2020s   | 10          |
| matmul     | matjuice      | node        | 0.1624s   | +-5.15%  | 0.1480s   | 0.1790s   | 20          |
| matmul     | matlab-concat | matlab-vm   | 1.1358s   | +-2.79%  | 1.0970s   | 1.2005s   | 10          |
| mcpi       | matjuice      | chrome      | 1.0879s   | +-4.40%  | 1.0250s   | 1.1630s   | 10          |
| mcpi       | matjuice      | firefox     | 4.2890s   | +-3.80%  | 4.0650s   | 4.5420s   | 10          |
| mcpi       | matjuice      | node        | 4.8038s   | +-4.16%  | 4.5340s   | 5.1450s   | 10          |
| mcpi       | matlab-concat | matlab-vm   | 2.9500s   | +-5.37%  | 2.7383s   | 3.2169s   | 10          |
| nb1d       | matjuice      | chrome      | 4.4567s   | +-8.10%  | 4.0800s   | 5.3080s   | 10          |
| nb1d       | matjuice      | firefox     | 6.4153s   | +-6.67%  | 5.9000s   | 7.2990s   | 10          |
| nb1d       | matjuice      | node        | 5.6276s   | +-14.37% | 5.1940s   | 7.9010s   | 10          |
| nb1d       | matlab-concat | matlab-vm   | 1.5517s   | +-4.06%  | 1.4192s   | 1.6401s   | 10          |
| numprime   | matjuice      | chrome      | 6.0603s   | +-1.29%  | 5.9710s   | 6.1180s   | 3           |
| numprime   | matjuice      | firefox     | 6.3777s   | +-0.38%  | 6.3500s   | 6.3940s   | 3           |
| numprime   | matjuice      | node        | 6.0267s   | +-0.88%  | 5.9680s   | 6.0710s   | 3           |
| numprime   | matlab-concat | matlab-vm   | 66.9836s  | +-0.51%  | 66.7685s  | 67.3755s  | 3           |

# Expressed as slowdowns compared to the MATLAB VM

### Invariants (configuration parameters that are the same for all runs) ###

| category       | short-name |
| -------------- | ---------- |
| implementation | matlab     |
| platform       | mba-2011   |
| input-size     | medium     |
Ratio:
    slowdown = mean-time / (reference mean-time)
Reference (used for computing the ratio):
    environment: matlab-vm
    compiler: matlab-concat

### Results ###

| benchmark  | compiler | environment | slowdown |
| ---------- | -------- | ----------- | -------- |
| babai      | matjuice | chrome      | 7.92x    |
| babai      | matjuice | firefox     | 6.62x    |
| babai      | matjuice | node        | 8.08x    |
| bubble     | matjuice | chrome      | 0.29x    |
| bubble     | matjuice | firefox     | 0.26x    |
| bubble     | matjuice | node        | 0.29x    |
| capr       | matjuice | chrome      | 0.30x    |
| capr       | matjuice | firefox     | 0.58x    |
| capr       | matjuice | node        | 0.29x    |
| clos       | matjuice | chrome      | 353.00x  |
| clos       | matjuice | firefox     | 366.87x  |
| clos       | matjuice | node        | 320.33x  |
| collatz    | matjuice | chrome      | 0.14x    |
| collatz    | matjuice | firefox     | 0.15x    |
| collatz    | matjuice | node        | 0.40x    |
| crni       | matjuice | chrome      | 4.68x    |
| crni       | matjuice | firefox     | 4.98x    |
| crni       | matjuice | node        | 4.11x    |
| dich       | matjuice | chrome      | 0.22x    |
| dich       | matjuice | firefox     | 0.21x    |
| dich       | matjuice | node        | 0.47x    |
| fdtd       | matjuice | chrome      | 599.96x  |
| fdtd       | matjuice | firefox     | 186.98x  |
| fdtd       | matjuice | node        | 382.34x  |
| fft        | matjuice | chrome      | 0.31x    |
| fft        | matjuice | firefox     | 0.53x    |
| fft        | matjuice | node        | 0.28x    |
| fiff       | matjuice | chrome      | 0.29x    |
| fiff       | matjuice | firefox     | 0.41x    |
| fiff       | matjuice | node        | 0.27x    |
| lgdr       | matjuice | chrome      | 1.66x    |
| lgdr       | matjuice | firefox     | 2.33x    |
| lgdr       | matjuice | node        | 3.36x    |
| makechange | matjuice | chrome      | 0.27x    |
| makechange | matjuice | firefox     | 0.54x    |
| makechange | matjuice | node        | 0.25x    |
| matmul     | matjuice | chrome      | 0.15x    |
| matmul     | matjuice | firefox     | 0.16x    |
| matmul     | matjuice | node        | 0.14x    |
| mcpi       | matjuice | chrome      | 0.37x    |
| mcpi       | matjuice | firefox     | 1.45x    |
| mcpi       | matjuice | node        | 1.63x    |
| nb1d       | matjuice | chrome      | 2.87x    |
| nb1d       | matjuice | firefox     | 4.13x    |
| nb1d       | matjuice | node        | 3.63x    |
| numprime   | matjuice | chrome      | 0.09x    |
| numprime   | matjuice | firefox     | 0.10x    |
| numprime   | matjuice | node        | 0.09x    |
