# Parallel processing in R
### Background
Can run in parallel tasks on a single host, parallel tasks on multiple hosts.  makeCluster() supports a large number of cluster types however FORK (for UNIX) and PSOCK (for Windows) are the standard mechanisms.  FORK is more memory efficient as UNIX supports shared copy-on-write.

For multiprocessor config
```
> library(doMC)
> registerDoMC(cores=8)
```
For workstation farm config
```
> makeCluster(3) -> myclust
> registerDoParallel(myclust)
...
> stopCluster(myclust)
```
```
> makeCluster
function (spec, type = getClusterOption("type"), ...) 
{
    switch(type, PSOCK = makePSOCKcluster(spec, ...), FORK = makeForkCluster(spec, ...), 
    SOCK = snow::makeSOCKcluster(spec, ...), MPI = snow::makeMPIcluster(spec, ...), 
    NWS = snow::makeNWScluster(spec, ...), stop("unknown cluster type"))
}
<bytecode: 0x5654c12ff168>
<environment: namespace:parallel>
```

Some useful sites:
* http://gforge.se/2015/02/how-to-go-parallel-in-r-basics-tips/
* http://www.parallelr.com/r-gpu-programming-for-all-with-gpur/
* [Parallel processing in caret](http://topepo.github.io/caret/parallel-processing.html)

### An example
```
> library(foreach)
library(doParallel)

# Setup the cluster
>makeCluster(3) -> myclust
summary(myclust)
registerDoParallel(myclust)

# modellist is a shared variable
>modellist <- list()
clusterExport(myclust, modellist)

# for loop in parallel
system.time(for (ntree in c(1000, 1500, 2000, 2500)) {
  set.seed(seed)
  train(Class~., data=dataset, method="rf", metric=metric, tuneGrid=tunegrid, trControl=trainControl, ntree=ntree) -> fit
  toString(ntree) -> key
  fit -> modellist[[key]]
})

# Checkout the results
summary(modellist)
results <- resamples(modellist)

plot(modellist[["1000"]])
plot(modellist[["1500"]])
plot(modellist[["2000"]])
plot(modellist[["2500"]])

# cleanup
stopCluster(myclust)
```
