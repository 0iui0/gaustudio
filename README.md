<p align="center">
    <picture>
    <img alt="gaustudio" src="" width="50%">
    </picture>
</p>


<p align="center"> <b>GAUStudio is a unified framework that supports the rapidly advancing field of 3D Gaussian Splatting (3DGS) and its applications. This framework targets to offer a comprehensive codebase, streamlined pipelines, and a wide range of tools and resources to facilitate the exploration, implementation, and deployment of 3DGS-based solutions, making it easier for users to leverage the potential of this cutting-edge technology.</b> </p>


### [Project Page (Coming Soon)]() | [Paper(Coming Soon) ]() | [Colab(Comming Soon)]()
<br/>

# Installation
Before installing the software, please note that the following steps have been tested on Ubuntu 20.04. If you encounter any issues during the installation on Windows, we are open to addressing and resolving such issues.

## Prerequisites
* NVIDIA graphics card with at least 6GB VRAM
* CUDA installed
* Python >= 3.8

## Optional Step: Create a Conda Environment
It is recommended to create a conda environment before proceeding with the installation. You can create a conda environment using the following commands:
```sh
# Create a new conda environment
conda create -n gaustudio python=3.8
# Activate the conda environment
conda activate gaustudio
```

## Step 1: Install PyTorch
You will need to install PyTorch. The software has been tested with torch1.12.1+cu113 and torch2.0.1+cu118, but other versions should also work fine. You can install PyTorch using conda as follows:
```
# Example command to install PyTorch version 1.12.1+cu113
conda install pytorch=1.12.1 torchvision=0.13.1 cudatoolkit=11.3 -c pytorch

# Example command to install PyTorch version 2.0.1+cu118
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118
```

## Step 2: Install Dependencies
Install the necessary dependencies by running the following command:
```sh
pip install -r requirements.txt
```

## Optional Step: Install PyTorch3D
If you require mesh rendering and further mesh refinement, you can install PyTorch3D follow the [link](https://github.com/facebookresearch/pytorch3d/blob/main/INSTALL.md):

# QuickStart
## Mesh Extraction for 3DGS 
### Prepare the input data
We currently support the output directory generated by most gaussian splatting methods such as [3DGS](https://github.com/graphdeco-inria/gaussian-splatting), [mip-splatting](https://github.com/autonomousvision/mip-splatting), [GaussianPro](https://github.com/kcheng1021/GaussianPro) with the following minimal structure:
- output_dir
    - cameras.json (necessary)
    - point_cloud 
        - iteration_xxxx
            - point_cloud.ply (necessary)

We are preparing some [demo data(comming soon)]() for quick-start testing. 

### Running the Mesh Extraction
To extract a mesh from the input data, run the following command:
```
gs-extract-mesh -m ./data/1750250955326095360_data/result -o ./output/1750250955326095360_data
```
Replace `./data/1750250955326095360_data/result` with the path to your input output_dir.
Replace `./output/1750250955326095360_data` with the desired path for the output mesh.

### Binding Texture to the Mesh
The output data is organized in the same format as [mvs-texturing]{https://github.com/nmoehrle/mvs-texturing/tree/master}. Follow these steps to add texture to the mesh:

* Compile the mvs-texturing repository on your system.
* Navigate to the output directory containing the mesh.
* Run the following command:
```
texrecon ./images ./fused_mesh.ply ./results/textured_mesh --outlier_removal=gauss_clamping --data_term=area --no_intermediate_results
```
