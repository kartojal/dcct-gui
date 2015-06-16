# dcct-gui
DCCT Tools front-end via Bash &amp; Zenity, by Kartojal.  Thanks to DCCT and Mirkic7 for the binaries!

# Features
  - Simple front end
  - Only one dependency: Zenity (Already installed in Ubuntu)
  - Bash binary script (you don't need to run a console for execute it))
  - Choose a DCCT tool from the list, and follow the windows to run it.
  - Plot Burst files without console skills. Plot supports SSE4 and AVX2 by Mirkic7.
  - Mine Burst without console, just select "Mine Burst", write the pool IP and select the plot directories, them        Whoala, dcct miner will run.
  - Optimize plots with only selecting the plot file.


# Easy How-To
  1. Download the pack with dcct + frontend from [here](https://mega.nz/#!a8c3GbiS!cdYOnjclPl7IM2uzd9jJaGFMAE3ag_yH7W3ove8bZUE).
  2. Uncompress it.
  3. Double click on "dcct-gui".

# To-do
  - Multi-arch (Now only 64 bits, soon one script for 32/64/ARM )
  - DCCT dev pools 2 Miner
  - [...]

# How-to compile this bash script  it to binary
  You can compile a bash script to binary, with shc by " Francisco Javier Rosales García "
  1. Go here http://www.datsi.fi.upm.es/~frosal/
  2. Download shc-3.8.9.tgz, uncompress, navigate to the dir, compile it ( make on console)
  3. Then, with that tool, just do:
    shc -f dcct-gui
  4. Now you have dcct-gui script compiled in C!
