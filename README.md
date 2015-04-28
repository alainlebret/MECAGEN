## MecaGen - A Simulation Platform of Animal Embryogenesis

[MecaGen](http://www.mecagen.org) is a C++ simulation platform of animal multicellular development relying on a realistic agent-based model. It is centered on the physico-chemical coupling of cell mechanics with gene expression and molecular signaling.

This project aims to investigate the multiscale dynamics of the early stages of biological morphogenesis. Embryonic development is viewed as an emergent, self-organized phenomenon based on a myriad of cells and their genetically regulated, and regulating, biomechanical behavior.

### 1. Installing on Linux

#### 1.1. Dependencies

Installing MecaGen requires a few libraries to be installed first. We recommend using a package manager such as "pacman" on Archlinux, or the "Advanced Packaging Tool" (APT) on Ubuntu and Debian. For the last two, you can copy and paste the following command in a terminal window:

```shell
sudo apt-get install libsdl2-dev libglew-dev freeglut3-dev libboost-serialization-dev libboost-random-dev qt5-default
```

These libraries can also be installed manually via the websites below:

* <a href="https://www.libsdl.org/release/SDL2-2.0.3.tar.gz" target="_blank">Simple DirectMedia Layer (SDL 2.0)</a>
* <a href="https://sourceforge.net/projects/glew/files/glew/1.12.0/glew-1.12.0.tgz/download" target="_blank">The OpenGL Extension Wrangler Library (GLEW)</a>
* <a href="http://sourceforge.net/projects/freeglut/files/freeglut/3.0.0/freeglut-3.0.0.tar.gz" target="_blank">The OpenGL Utility Toolkit (GLUT)</a>
* <a href="http://sourceforge.net/projects/boost/files/boost/1.55.0/boost_1_55_0.tar.gz/download" target="_blank">Boost</a>
* <a href="" target="_blank"></a>
* <a href="" target="_blank"></a>
* <a href="" target="_blank"></a>
* GLEW ([The OpenGL Extension Wrangler Library](http://glew.sourceforge.net/))
* GLUT ([The OpenGL Utility Toolkit](https://www.opengl.org/resources/libraries/glut/))
* [Boost Serialization](http://www.boost.org/doc/libs/1_57_0/libs/serialization/doc/index.html) 
* [Boost Random Number Library](http://www.boost.org/doc/libs/1_57_0/doc/html/boost_random.html)
* [QT5.x](http://qt-project.org/downloads)

Then, if your machine is equipped with an NVIDIA graphics card, we recommend to install the CUDA library:

```shell
sudo apt-get install nvidia-cuda-toolkit
```

* [CUDA 5.5](https://developer.nvidia.com/cuda-toolkit-55-archive) or newer



* (Required only if no Cuda is installed) [Thrust](http://thrust.github.io/)

Thrust is included with Cuda. Yet if you install MecaGen without Cuda, the Thrust header library must be installed manually. Thrust is a C++ template library so the files just need to be copied on your system.

#### 1.2. Environment variables

The QT library folder must be in the LIBRARY_PATH environment variable and the folder containing the Meta-Object Compiler (moc) program in the PATH environment variable.

Cuda is required to enable an enhanced rendering of the simulations. It uses Vertex Buffer Object to interoperate with OpenGL. The folder containing the Nvidia Cuda Compiler (nvcc) must be in the PATH environment variable.

First, edit the user paths file [(user_paths_MUST_BE_EDITED_FIRST)](user_paths_MUST_BE_EDITED_FIRST) by specifying your installation paths for QT, and Cuda or Thrust. If Cuda is installed on your system, we recommend that you compile MecaGen with the VBO/Cuda version of the cells rendering by using the first option in the file.

#### 1.3. Compilation

Then, decide which custom version of MecaGen you want to use. Indeed, one of the specificities of the MecaGen platform is the possibility to integrate external customization code to simulate specific structures and behaviors such as for example extra-embryonic tissue. Currently, two custom versions are available: the "default" custom version performs regular MecaGen simulation without specific structure or behavior, and the "zebrafish" custom version adds rules for the yolk cell and the enveloping layer. 

It is not currently possible to compile both custom version at the same time so you have to choose whether you want to compile the default version with the [parent makefile](Makefile)

```shell
make CUSTOM=default
```

or the zebrafish version

```shell
make CUSTOM=zebrafish
```

When you switch between the two custom versions, all generated files must be cleaned from your system with the following command

```shell
make propper
```

### 2. Generate and run examples

MecaGen use xml files as inputs for the simulations. Three input files are required: 
- a *parameter* file containing all the parameters describing the gene regulatory network, the molecular interactions, and the biomechanical properties,
- a *state* file containing the initial state of the variables,
- a *meta-parameter* file containing information related to algorithmic or rendering options.

#### 2.1. Generate input files

For a simulation consisting of a large number of cells, it is not practical to generate the *parameter* and *state* file by hand. We provide in the following short C++ programs allowing their generation.

The examples' input files are generated by the [generate_input_files.sh](mecagen/generate_input_files.sh) script. It takes a single argument according to whether all, or some, input files are to be generated:

```shell
cd mecagen
./generate_input_files.sh all
```

or

```shell
cd mecagen
./generate_input_files.sh default
```

or

```shell
cd mecagen
./generate_input_files.sh zebrafish
```

#### 2.2. Run examples

Once input files are generated, MecaGen simulations can be started by running the [run_examples.sh](mecagen/run_examples.sh) script. If the execution returns prematurely with "gpuassert", please start the script with sudo: "sudo run_examples.sh".

#### 2.3. Support videos

Two videos demonstrate the previous instructions and are accessible on youtube:

* the [first video](https://www.youtube.com/watch?v=d79v7MDPIBw) details the procedure required to compile and run the "zebrafish" mode simulation with Cuda/VBO rendering.
* the [second video](https://www.youtube.com/watch?v=5zcLAL-caDQ) details the procedure required to compile and run the "default" mode simulations without the Cuda/VBO rendering. 

## 3. License

MecaGen is released under the GNU General Public License v3.0; see LICENSE for more details.