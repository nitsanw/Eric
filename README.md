# Eric
A benchmark result repository for tracking performance over time. 

## Database
Benchmark results are stored in a database with the following entities/relationships:

__benchmark__  
benchmark id  
suite  
name  
tags  

__config__  
config id  
jvm/jdk  
command line parameters  
configuration files  
build number  

__machine__  
machine id  
hostname  
OS  

__run__  
run id  
benchmark id  
machine id  
config id  
time  

__result__  
result id  
run id  
type  
score  

__regression__  
regression id  
since result id
until result id  
link to issue system  
acceptable  

## What the data means
The bulk of the data in the Eric database will be runs and results. A run will capture a single execution of the experiment/benchmark including it's configuration data, versions and execution environments. The scheme should be expanded to support further relevant variables. Each run will have 1 or more results which will be used to compare the run with other runs.

## Making useful comparisons
Eric will provide reporting capabilities on top of the data:  
 * Compare the results of several benchmarks representing alternative implementations of same/similar functionality.
 * Compare the results of same benchmark over time.
 * Compare benchmark results across JVM/OS/Machine/Configuration.
 * Report results as percentage of some baseline measurement/target

## Detecting regressions
Eric will provide regression detection capabilites:
 * Is a given run better/worse than 'last' run within some margin?
 * Establish 'normal' result variance based on data
 * Better/worse depending on result type (e.g time/throughput/histogram/footprint/cpu-usage)
 * Detect slow regressions over time

## Tracking regressions
Tracking regressions across a large benchmark suite requires the ability to report on the following benchmark states:
 * Improved - on occassion, things get better, it nice to know when and why.
 * Stable - most runs should show no regression/improvement. Small incremental changes...
 * New regression - we stumbled somewhere between A and B, sound the bells
 * Ongoing regression - maybe we're still looking into it, but this benchmark is broken. Ongoing regressions can get worse too, changing state to new regression. 
 * Resolved - we went from regression to previously observed stable result. Or maybe we just accepted the regression (perhaps the fast solution was due to a bug).
