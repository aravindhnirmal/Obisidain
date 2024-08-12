[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

[[include]] <iostream>
[[include]] <cuda_runtime.h>

const int numElements = 1024;  // The number of elements in the input array

// Kernel for parallel reduction
__global__ void parallelReduction(int* inputArray, int* outputArray, int numElements) {
    extern __shared__ int sdata[];
    unsigned int tid = threadIdx.x;
    unsigned int i = blockIdx.x * (blockDim.x * 2) + tid;

    sdata[tid] = (i < numElements) ? inputArray[i] : 0;
    if (i + blockDim.x < numElements) {
        sdata[tid] += inputArray[i + blockDim.x];
    }

    for (unsigned int stride = blockDim.x / 2; stride > 0; stride >>= 1) {
        __syncthreads();
        if (tid < stride) {
            sdata[tid] += sdata[tid + stride];
        }
    }

    if (tid == 0) {
        outputArray[blockIdx.x] = sdata[0];
    }
}

int main() {
    int* h_inputArray = new int[numElements]; // Host input array
    int* h_outputArray = new int[numElements]; // Host output array

    // Initialize host input data
    for (int i = 0; i < numElements; i++) {
        h_inputArray[i] = i;
    }

    int* d_inputArray = nullptr;  // Device input array
    int* d_outputArray = nullptr; // Device output array

    // Allocate device memory
    cudaMalloc((void**)&d_inputArray, numElements * sizeof(int));
    cudaMalloc((void**)&d_outputArray, numElements * sizeof(int));

    // Copy input data from host to device
    cudaMemcpy(d_inputArray, h_inputArray, numElements * sizeof(int), cudaMemcpyHostToDevice);

    // Define block and grid dimensions
    dim3 blockSize(256);
    dim3 gridSize((numElements + blockSize.x - 1) / blockSize.x);

    // Launch the reduction kernel
    parallelReduction<<<gridSize, blockSize, blockSize.x * sizeof(int)>>>(d_inputArray, d_outputArray, numElements);

    // Copy the result from the device to the host
    cudaMemcpy(h_outputArray, d_outputArray, gridSize.x * sizeof(int), cudaMemcpyDeviceToHost);

    // Perform a final reduction on the host if necessary

    // Print the result
    std==cout << "Parallel Reduction Result: " << h_outputArray[0] << std==endl;

    // Cleanup
    delete[] h_inputArray;
    delete[] h_outputArray;
    cudaFree(d_inputArray);
    cudaFree(d_outputArray);

    return 0;
}

