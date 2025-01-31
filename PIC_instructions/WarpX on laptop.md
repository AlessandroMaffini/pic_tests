# Documentation 
https://ecp-warpx.github.io/
https://warpx.readthedocs.io/en/latest/

# Build
clone repository and move there 
```
git clone https://github.com/ECP-WarpX/WarpX.git warpx
cd warpx
```

source Spack if you don't do it in your `bash.rc` 
```
source $SPACK_DIR/share/spack/setup-env.sh
```

activate warpx environment
```
spack env activate -p myspackwarpx
``` 

configure build 
```
cmake -S . -B build
```

if you need change the configuration options (e.g. choose dimensionality - default is 3D, GPU support vs. CPU only)
```
ccmake build
```

build
```
cmake --build build -j 2
```

# Run 
copy the executable you find in `/warpx/build/bin` (e.g. `warpx.2d.MPI.OMP.DP.PDP.OPMD.QED`) and an input file (input.py) in a directory (mydir) and move there 
set the number of threads per core depending on the machine 
```
export OMP_NUM_THREADS=2
```
run on 4 cores dividing the simulation box in 1x4 subgrids 
```
mpirun -np 4 ./warpx.2d.MPI.OMP.DP.PDP.OPMD.QED input.txt warpx.numprocs = 1 4
```
note that the `warpx.numprocs` flag is optional

# Analyze
install openpmd as
```
pip install openpmd-api
```

now you should have the necessary software to post-process warpx data with python, i.e. in a python file you can now do 
```
import openpmd_api as io
```

refer to:
http://www.openpmd.org/
https://openpmd-api.readthedocs.io/en/latest/


# Build and run on GPU
