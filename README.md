This repository contains all instructions on how to use the artefact going along with the paper "Generating Customised Control Flow Graphs for Legacy Languages with Semi-Parsing", that will be presented and published at ICSME2022. A copy of the camera-ready paper is provided. Abstract: *We propose a tool and underlying technique that uses semi-parsing to extract control flow graphs from legacy source code (i.e., COBOL).
Obtaining such control flow graphs is relevant in the industrial setting of legacy modernisation, to quickly demonstrate to code owners that modernisation engineers did not break their business logic.
They need to be convinced that a migration did not affect the flow around critical parts of their code such as database accesses. Focusing on the control flow around embedded SQL queries and confirming that the code logic has been preserved improves customers' trust and satisfaction in the modernisation.
Our proposed algorithm and approach uses fuzzy parsing as opposed to full parsing to parse mainly the control flow constructs, while delegating the full parsing of embedded languages like SQL to an external parser, and produces a control flow graph directly while skipping over most of the input in linear time. Such a fuzzy parser is easier to construct and adapt to particular languages and needs than a full parser with a visitor to elicit control flow. Comparisons are made of the fuzzy parser to an industrial-strength full parser.*

# What does the artifact do ?

This artifact is available in two versions: either a local install or an Ubuntu VM. The installation process will allow you to download our fuzzy parsing tool along with the public files that we used to perform our tests (our test files and the NIST files). Not included in this artefact are the Raincode COBOL compiler and the client project we ran our tool on. The project files are confidential, but the Raincode compiler is available for free [on their website](https://www.raincode.com/download/) when requested if you wish to try that as well. 

In the artefact, we include a tutorial on how to run our tool, which creates PDFs of generated CFGs using graphviz, as well as an explanation on how to test the performance of our tool. Note that the comparison with the Raincode parser is not possible without requesting and installing it, we therefore provide a script to run the performance testing for our tool only. Csv files containing the results of the performance testing described in our paper are available in the result directory.

# How do I install this artefact ?

All the details on the installation process are in our [INSTALL.md](https://github.com/CelineDknp/ICSMEArtefact/blob/main/INSTALL.md) file. In summary, if you want to use our provided VM, it is available on Zenodo, at [this link](https://zenodo.org/deposit/6806075). Simply download the file, unzip it, and load it into VirtualBox. If you want to perform a local install, you can pull from the ICSME-Artefact branch on [our GitHub](https://github.com/CelineDknp/SemiParsingCFG) and install all the requirements.

# How to reproduce the results found in the paper ?

## Get the CFGs

If you want to generate the CFG for any given file simply go to the `SemiParsingCFG` directory (on the Desktop of your VM, or where you installed it locally) and run `python src/main.py path_to_file` or `python3 src/main.py path_to_file` depending on the alias for Python3 on your machine. This will create two files: *filename.pdf*, that contains the visualisation of the CFG, as well as *filaname.gv*, that contains the description of the graph in the `DOT` format.

For example, to get the CFG shown in Fig. 3 of our paper, run `python3 src/main.py TestFiles/pytest/if_left_branch_test_file.COB` and to get the CFG for the first NIST file, run `python3 main.py TestFiles/NIST/IC101A.cob`.

## Run the performance tests

If you want to test the performance of our tool, in the same `SemiParsingCFG` directory, you can run our `perf_test_fuzzy.py` file. This will create a csv file containing the average execution time for our parser on either a single file or all files in a directory. The base use is `python3 src/perf_test_fuzzy.py file_or_directory_path (-dir) output_file.csv`. The `-dir` flag is necessary when you want to compute the performance for the content of a directory and not a single file. Other non-mandatory arguments are:

-  `-batch`: this will run the tests in batches, meaning that a single instance of the parser will be created and run all the files one after the other. This is a significant speedup for the performance testing itself, we therefore advise you to use it.
- `-thread N`: this allows you to specify how many threads you want to run in parallel for the performance testing. By default, a single thread is used. To run with 4 threads for example, write `-thread 4`. This also speeds up significantly the time needed to compute the performance tests.
- `-runs M`: this allows you to modify the number of runs (repetitions of the parsing) for each file. The default number is 20, as used in our paper. To reduce this to 10 for example, write `-runs 10`.

>Note that, if you are running on the VM, there are only 2 available CPU threads and 4Go of memory, so we advise to be careful with how many threads you create. If your computer is powerful enough, you can change the settings in VirtualBox.

For example, run `python3 src/perf_test_fuzzy.py TestFiles/pytest -dir output_file.csv -batch` to get the performance for parsing our test suite.

## Performance tests used in our paper

Since we can't ship the Raincode parser in the VM to allow a full reproduction of the tests described in our paper, we include in the `result` directory the .csv files generated by our `perf_test.py` script (same functionnalities as `perf_test_fuzzy.py` with the addition of running the Raincode parser and comparing the times). You will find four files describing the performances for: the test files, the NIST files and the migration project (separated in V1 and V2). The average execution time for each file for each parser is present, with at the end the sum over all files, as described in our paper on Table 1. Note that these were run with our scripts pre-compiled by nuitka, and with the `-batch` flag.


