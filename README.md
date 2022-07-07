# What does the artifact do ?

This artifact is available in two versions: either a local install or an Ubunto VM. The installation process will allow you to download out fuzzy parsing tool along with the public files that we used to perform our tests (our test files and the NIST files). Not included in this artefact are the Raincode COBOL compiler and the client project we ran our tool on. The project files are confidential, but Raincode's compiler is available for free [on their website](https://www.raincode.com/download/) when requested. 
In the artefact, we include a tutorial on how to run our tool to create PDFs of generated CFGs using graphviz as well as an explanation on how to test the performance of our tool. Note that the comparison with the Raincode parser is not possible without requesting and installing it, we therefore provide a script to run the performance testing for the fuzzy parsing only. Csv files containing the results of the performance testing described in our paper are available as well in the [] directory.

# How do I install this artefact ?

If you want to go that route, the VM is available on Zenodo in open access, at [this link](). Simply download the file, unzip it, and load it into VirtualBox. If you want to perform a local install or more detail on the installation process, see our [INSTALL.md]() file.

# How to reproduce the results found in the paper ?

## Get the CFGs

If you want to generate the CFG for any given file simply go in the `SemiParsingCFG` directory (on the Desktop of your VM, or where you installed it locally) and run `python src/main.py "path_to_file"` or `python3 src/main.py "path_to_file"`. 

For example, to get the CFG shown in Fig. 3 of our paper, run `python3 src/main.py "TestFiles/pytest/if_left_branch_test_file.COB"` and to get the CFG for the first NIST file, run `python3 main.py "COBOL_85/IC101A.cob"`.

## Run the performance test

If you want to test the performance of our tool, in the same `SemiParsingCFG` directory, you can run `python3 perf_test_fuzzy.py -d Cobol_85 output_file.csv`. This will create a csv file containing the average execution (over 10 executions) time for our parser on all files in the *Cobol_85* directory. This can also be run for a single file (without the -d parameter). 
