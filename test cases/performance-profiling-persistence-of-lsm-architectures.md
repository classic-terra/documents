# Test Case - Performance profiling persistence of LSM architecture

## Objectives
Read / write amplification are major problems in many LSM-trees implementations, like LevelDB. Read / Write amplification is defined as the ratio between the amount of data written to (or read from) the underlying storage device vs the amount of data requested by the user. The "amplification problem" has been a major issues for LSM-trees for a while. There are two sources of read / write amplification in systems such as LevelDB. First, to lookup a key-value pair, LevelDB may need to check multiple levels. In the worst case, LevelDB needs to check eight files in L0, and one file for each of the remaining six levels: a total of 14 files. Second, to find a key-value pair within a SSTable file, LevelDB needs to read multiple metadata blocks within the file. Specifically, the amount of data actually read is given by (index block + bloom-filter blocks + data block). For example, to lookup a 1-KB key-value pair, LevelDB needs to read a 16-KB index block, a 4-KB bloom-filter block, and a 4-KB data block; in total, 24 KB. Therefore, considering the 14 SSTable files in the worst case, the read amplification of LevelDB is 24 × 14 = 336. 

The purpose of this test case is to profile how the targeted KVStores supported by Cosmos SDK (RocksDB, PebbleDB & BadgerDB) perform under various scenarios with differents loads, key ordering and payload sizes in order to play to the strengths & weaknesses of the targeted KVStore implementations to benchmark the performance characteristics (cpu, memory, gc, threads, mutexes, etc) of their individual "compaction algorithms".

## Preconditions
Our test scenario has no pre-conditions because the features can be tested in isolation and rely on standard GoLang tooling. As such we have noticed some breakage in the Terra Classic code when we use various flags, e.g. ´--bench´, which might require us to upgrade unit tests as we encounter problems in the existing test code. But by and large our test case is not very complex, as it focuses primarly on profiling the interaction between the underlying Cosmos SDK / Tendermint SDK dependencies, which means we can simply choose to work-around these issues and test the 3rd party dependencies directly. 


## Input Specifications 
We need to compile benchmarking data for various test scenarios that will be run against the targeted KVStore in order to profile them individually and subsequently assess the optimal trade-off for Terra Classics requirements. By and large we want to focus the test on bootstrapping data that has either "pre-ordered" key data or "unordered" key data to be able to measure the overhead of in-memory sorting before KV pairs are "flushed" to the underlying SSTables. Furthermore we want to alternate the payload sizes in order figure out how the different "compaction algorithms" perform on the subject of read / write amplication in order to determine what is the optimal architecture for Terra Classic.

### Data sources
In general data should be generated using some sort of "fuzzy logic" to ensure we dont end up measuring "golden path scenarios" where KVStore compression allow BLOBs to be compressed to the point where they are inherently negligable in size due to the process of "tokenization" that takes place in data compression algorithms. Data sources such as "image data" & "smart contract code" offers a high degree of "fuzziness" out-of-the-box while also represent a large sample of the data that is stored on mainnet, making them prime candidates as "test data sources".

Our test case we will target the following payload sizes / "value types":

- Sequence of pre-orderered keys with corresponding 8B "image values"
- Sequence of unordered keys with corresponding 8B "image values"
- Sequence of pre-orderered keys with corresponding 8KB "image values"
- Sequence of unordered keys with corresponding 8KB "image values"
- Sequence of pre-orderered keys with corresponding 64KB "image values"
- Sequence of unordered keys with corresponding 64KB "image values"
- Sequence of pre-orderered keys with corresponding 4GB "cosmwasm values"
- Sequence of unordered keys with corresponding 4GB "cosmwasm values"

## Output Specification
The desired outputs of our benchmarking efforts focus primarily on KPIs that are native to the GoLang subroutines performing compaction for the "persistency layer" as this is where we assume the read / write amplification is most prevailent. Initially our focus will be on the following KPIs, however this can be extended as we progress thru the workload:

- CPU utilization
- Memory allocation
- Creation of OS threads
- Blocking on synchronization primitives
- Holders of contended mutexes

Disc I/O has intentionally been left out as Notional Labs has already done extensive (excellent) work on that subject and concluded that PebbleDB is by and large the most high performent database available in the market. However as such PebbleDB is optimized for "reading small values fast" (optimized for Facebook, which tends to favor "read performance & eventual consistency" over "write performance") which means it might not deal with the process of "compaction" (read + write amplification) as efficiently as alternatives like BadgerDB once the payload sizes grow above a certain size (> 64KB). As a general conclusion we are hoping to determine how these "hybrid LSM-tree architetures" deal with the afformentioned challenges under different scenarios.

## Post Conditions
Upon completion of the test case we will have achieved consensus in the L1 Task Force on which KVStore archictures work well for what use cases so we can make a collective decission on how to best position Terra Classic for the future "data scalability" issues inherent to the Cosmos SDK architecture.

## Hardware
As we have intentionally left out the disc I/O KPI the testy cases does not have any hardware requirements. It is however important that the tests are performed on the same physical hardware.

## Software
The primary requirement on the software front is deciding on the OS which will be Ubuntu and Alpine to keep  it centered on Linux distrobutions that are used by the validator pillar in the Terra Classic network. Furthermore we will utilize the built-in GoLang profiling tools (go test, pprof, etc).

## Procedural Requirements
None

## Others
None

## Intercase Dependencies
No intercase dependencies
