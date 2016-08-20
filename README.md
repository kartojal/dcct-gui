# dcct-gui
DCCT Tools front-end via Bash &amp; Zenity, by Kartojal.  Thanks to DCCT and Mirkic7 for the binaries!

# Features
  - Simple front end
  - Only one dependency: Zenity (Already installed in Ubuntu and Linux Mint)
  - Choose a DCCT tool from the list, and follow the windows to run it.
  - Plot supports SSE4 and AVX2 by Mirkic7.
  - Optimize plots with only selecting the plot file.


# How-to
´´´
# git clone this repo and Mirkic7 mdcct repo
git clone https://github.com/kartojal/dcct-gui
git clone https://github.com/Mirkic7/mdcct

# go to mdcct directory and compile
cd mdcct
make

# copy the generated binaries to dcct-gui directory
cp mine mine_pool_all  mine_pool_share optimize plot plotavx2 ../dcct-gui

# go to dcct-gui directory, and launch dcct-gui script
cd ../dcct-gui
bash dcct-gui

´´´

