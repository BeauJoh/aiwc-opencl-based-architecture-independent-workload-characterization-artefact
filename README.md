
AIWC: OpenCL-based Architecture Independent Workload Characterization Artefact
------------------------------------------------------------------------------


[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/BeauJoh/aiwc-opencl-based-architecture-independent-workload-characterization-artefact/master)

#Installation

This project uses Docker to facilitate reproducibility. As such, it has the following dependencies:

* Docker -- available [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

Optional Dependencies:

* Cuda 9.0 Runtime -- available [here](https://developer.nvidia.com/cuda-downloads)
* nvidia-docker2, install instructions found [here](https://github.com/NVIDIA/nvidia-docker)
* Docker nvidia container, installed with: `sudo apt install nvidia-container-runtime`

#Build

To generate a docker image named aiwc-evaluation, run:

`docker build -t aiwc-evaluation .`

#Run

To start the docker image run:

`docker run --runtime=nvidia -it --mount src=`pwd`,target=/aiwc-evaluation,type=bind -p 8888:8888 --net=host aiwc-evaluation`

For reproducibility, BeakerX has also been added for replicating results and for the transparency of analysis.
To evaluate the artefact, launch jupyter with:

`beakerx --allow-root`

from within the container and following the prompts to access it from the website front-end.

*Note* that if this node is accessed from an ssh session local ssh port forwarding is required and is achieved with the following:

`ssh -N -f -L localhost:8888:localhost:8888 <node-name>`

#Investigation

If you wanted to run Oclgrind -- and AIWC -- on some fresh codes, the binary is located in /oclgrind/bin/oclgrind and the Extended OpenDwarfs Benchmark suite is located in /OpenDwarfs/build/
AIWC specific source-code can be found in: /oclgrind-source/src/plugins/WorkloadCharacterisation.cpp and /oclgrind-source/src/plugins/WorkloadCharacterisation.h
To run AIWC on any OpenCL code simply prepend the following to your OpenCL program binary with:

~~~~
cd /OpenDwarfs/build
$OCLGRIND_BIN --workload-characterisation ./csr -i ../test/sparse-linear-algebra/SPMV/tiny
cd /aiwc-evaluation
~~~~

