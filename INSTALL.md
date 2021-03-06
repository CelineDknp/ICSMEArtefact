# Install

Our tool is simply composed of Python scripts, so you can chose to either install it locally by pulling from our GitHub, or to grab the provided Ubuntu VM if you don't wish to install directly on your machine.

## Version A: Local install
Requirement for the local install: a git client, Python3 and pip must be installed. The install procedure is as follows:

1. Pull the code from our GitHub repository with `git clone https://github.com/CelineDknp/SemiParsingCFG.git`
2. Navigate to the directory where you cloned the repo, and run `git fetch` to make sure that you have all the branches, then either `git switch ICSME-Artefact` or `git checkout origin/ICSME-Artefact`.
3. Go into the `src` directory and run `pip install -r requirements.txt` (This should install pytest, graphviz and antlr4)
4. If you wish to generate the PDFs for the CFGs: install graphviz on your system. Follow the instructions corresponding to your OS that are available [here](https://graphviz.org/download/)

That's it, the project is installed ! To make sure that everything went smoothly, go back to the base directory (`cd ..`) and run the tests with `python3 -m pytest` or `python -m pytest`, depending on which alias calls Python3 on your machine. All tests should be green.


## Version B: VM install

1. If you don't have it already or have an older version, download [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Download our VM files [here](https://zenodo.org/deposit/6806075)
3. Unzip the files (somewhere easy to find)
4. Import the VM into your VirtualBox: Machine -> Add -> Navigate to our downloaded file -> Select the "FuzzyParsingICSMEArtifact.vbox" -> Open
5. Select the VM and click "Start"
6. Ubuntu is set up to automatically log in, so you should be set. If you ever need it, the admin password is simply "admin".
>Note: our VM is configured to run using minimal ressources, just 4GB of RAM and 2 CPU cores. It is sufficient to run our tool, but feel free to change those settings in the "System" tab of the VM if you have a more powerful computer.

>If you are using MacOS, and a fresh install of VirtualBox, you might run on some issue when launching the VM. A restart is often required, see [this page](https://www.howtogeek.com/658047/how-to-fix-virtualboxs-%E2%80%9Ckernel-driver-not-installed-rc-1908-error/) for more details.

>If you are using Windows 10, you might have to turn Hyper-V off as explained in [this tutorial](https://forums.virtualbox.org/viewtopic.php?f=25&t=99390). This would be the case if the VM shows only a black screen after starting it, and if there is a turtle in the icons on the lower-right side of the window. 

## Basic usage of our tool

If you installed the VM, start it. On the VM or your machine, navigate to the `SemiParsingCFG` (on the Desktop for the VM) and open a terminal.

1. To check that the install worked, run `python3 -m pytest` or `python -m pytest` (depending on which calls Python3)
2. To generate a CFG and view it, run `python3 src/main.py path_to_file`, e.g. `python3 src/main.py TestFiles/pytest/if_left_branch_test_file.COB`
3. To run the performance test on our fuzzy parser, launch `python3 src/perf_test_fuzzy.py TestFiles/pytest -dir output_file.csv -batch`

## Procedure tested
- On two Windows machines
