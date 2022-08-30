# AST

## Abstract 

The automated software testing technique fuzzing has seen a golden age in
the last decade, with widespread use in industry and academia. On the hunt
to find vulnerabilities, fuzzing binaries are compiled with default compiler
optimizations such as -O2, or -O3, which remain the hard-coded default in
popular fuzzers such as AFL++. On a binary level, software compiled from
the same source code may vastly differ in control flow depending on used
compilation flags. In this work, we aim to analyze the impact of different
compiler optimizations on the fuzzing process and provide further insight.
We influence compilation passes of the clang/LLVM compiler and analyze
their impact on the fuzzing performance of AFL++. We integrate our work
into Fuzzbench, an open-source fuzzing pipeline, and run experiments on
real-world benchmarks. Our preliminary fuzzing results indicate that there
is a delicate trade-off between runtime performance and code complexity.
While our results show significant differences on the scale of individual
benchmarks, when summarizing across the whole bench suite, there is no
evidence to suggest a statistical difference in fuzzing performance.

## Install
```
sudo apt-get install python3.8-dev python3.8-venv
sudo apt-get install rsync
make install-dependencies
make presubmit
make format
```




## Run Fuzzing
```
source .venv/bin/activate
```

```
PYTHONPATH=. python3 experiment/run_experiment.py  --experiment-config $EXPERIMENT_CONFIG_FILE --benchmarks freetype2-2017 bloaty_fuzz_target --experiment-name $EXPERIMENT_NAME --fuzzers afl libfuzzer 
```


## Links
Fuzzbench_fork: https://github.com/mattweingarten/fuzzbench <br />
af++_fork: https://github.com/mattweingarten/AFLplusplus <br />
Fuzzbench: https://google.github.io/fuzzbench/ <br />
LLVM flags: https://llvm.org/docs/Passes.html#id97 <br />
CLANG code coverage: https://clang.llvm.org/docs/SourceBasedCodeCoverage.html#id7 <br />

## Other Resources
- afl++ with modified command line args: https://github.com/abertschi/AFLplusplus/tree/ast/ast
  - pass clang args with AST_CC_ARGS="-O0" AFL_DONT_OPTIMIZE=1 ${CC} .

## Notes

```
PYTHONPATH=. python3 experiment/run_experiment.py --experiment-config ../AST/experiment-config.yaml  --experiment-name run14  --fuzzers aflo0 aflo1 aflo2 aflo3  
```

### Docker cleanup
```
alias docker-cleanup='docker ps -a -q | xargs -I {} docker rm {} ; docker images -q -f dangling=true | xargs -I {} docker rmi -f {}; docker volume ls -qf dangling=true | xargs -I {} docker volume rm {}'

```
