# Installing GROMACS with GPU Support

GROMACS is a powerful tool for simulating particle interactions in molecular dynamics. Leveraging GPU support can significantly enhance its performance. Follow this comprehensive guide to install GROMACS with GPU support and set it up as the default in your environment.

## Step 1: Install NVIDIA Drivers and CUDA

1. **Check GPU Compatibility**: Ensure your GPU is compatible with CUDA by referring to NVIDIA’s CUDA GPUs page.
2. **Install NVIDIA Drivers and CUDA Toolkit**:
    ```bash
    sudo apt update
    sudo apt install nvidia-cuda-toolkit
    ```
3. **Verify CUDA Installation**: Check the CUDA version with:
    ```bash
    nvidia-smi
    ```

## Step 2: Install Dependencies

Install the necessary packages for building GROMACS:
```bash
sudo apt update
sudo apt install cmake build-essential libfftw3-dev
```

## Step 3: Download GROMACS Source Code

Download the latest stable version of GROMACS from the official GROMACS website or use the following command:
```bash
wget ftp://ftp.gromacs.org/pub/gromacs/gromacs-2020.1.tar.gz
```
Extract the downloaded file:
```bash
tar -zxvf gromacs-2020.1.tar.gz
cd gromacs-2020.1
```

## Step 4: Configure and Build GROMACS with GPU Support

1. **Set Up a Build Directory**:
    ```bash
    mkdir build && cd build
    ```
2. **Configure with cmake**:
    ```bash
    cmake .. -DGMX_BUILD_OWN_FFTW=ON -DGMX_GPU=CUDA -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda -DGMX_CUDA_TARGET_COMPUTE=XX -DGMX_USE_OPENCL=OFF -DGMX_MPI=OFF -DGMX_OPENMP=ON
    ```
    Replace `XX` with the correct Compute Capability for your GPU (e.g., 75 for a GTX 1650).

3. **Build GROMACS**:
    ```bash
    make -j$(nproc)
    ```
4. **Install GROMACS**:
    ```bash
    sudo make install
    ```

## Step 5: Set Up GROMACS as Default

Add GROMACS to your shell’s startup configuration:
```bash
nano ~/.bashrc
```
Add the following line at the end of the file:
```bash
source /usr/local/gromacs/bin/GMXRC
```
Apply the changes:
```bash
source ~/.bashrc
```

## Step 6: Verify the Installation

Check the GROMACS version:
```bash
gmx mdrun --version
```
Ensure CUDA is listed in the output, indicating GPU support is enabled.

By following these steps, you’ll have GROMACS installed with GPU support, ready to enhance your molecular dynamics simulations. Happy computing!