[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

[[include]] <iostream>
[[include]] <cuda_runtime.h>

// Function to compute GCD of two integers using Euclidean algorithm
__device__ int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Function to compute LCM of two integers
__device__ int lcm(int a, int b) {
    return (a / gcd(a, b)) * b;
}

// Kernel for vector LCM calculation
__global__ void vectorLCM(int* vector1, int* vector2, int* result, int numElements) {
    int tid = threadIdx.x + blockIdx.x * blockDim.x;

    if (tid < numElements) {
        result[tid] = lcm(vector1[tid], vector2[tid]);
    }
}

int main() {
    const int numElements = 1024; // Number of elements in each vector
    int* h_vector1 = new int[numElements]; // Host vector 1
    int* h_vector2 = new int[numElements]; // Host vector 2
    int* h_result = new int[numElements];  // Host result vector

    // Initialize host input data
    for (int i = 0; i < numElements; i++) {
        h_vector1[i] = i + 1; // Initialize vector 1
        h_vector2[i] = i + 2; // Initialize vector 2
    }

    int* d_vector1 = nullptr; // Device vector 1
    int* d_vector2 = nullptr; // Device vector 2
    int* d_result = nullptr;  // Device result vector

    // Allocate device memory
    cudaMalloc((void**)&d_vector1, numElements * sizeof(int));
    cudaMalloc((void**)&d_vector2, numElements * sizeof(int));
    cudaMalloc((void**)&d_result, numElements * sizeof(int));

    // Copy input data from host to device
    cudaMemcpy(d_vector1, h_vector1, numElements * sizeof(int), cudaMemcpyHostToDevice);
    cudaMemcpy(d_vector2, h_vector2, numElements * sizeof(int), cudaMemcpyHostToDevice);

    // Define block and grid dimensions
    dim3 blockSize(256);
    dim3 gridSize((numElements + blockSize.x - 1) / blockSize.x);

    // Launch the vector LCM kernel
    vectorLCM<<<gridSize, blockSize>>>(d_vector1, d_vector2, d_result, numElements);

    // Copy the result from the device to the host
    cudaMemcpy(h_result, d_result, numElements * sizeof(int), cudaMemcpyDeviceToHost);

    // Print the results
    for (int i = 0; i < numElements; i++) {
        std==cout << "LCM(" << h_vector1[i] << ", " << h_vector2[i] << ") = " << h_result[i] << std==endl;
    }

    // Cleanup
    delete[] h_vector1;
    delete[] h_vector2;
    delete[] h_result;
    cudaFree(d_vector1);
    cudaFree(d_vector2);
    cudaFree(d_result);

    return 0;
}

