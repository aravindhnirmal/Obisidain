[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 


import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[][] matrix = new int[n][n];
        for (int i = 0; i < n; i++) {
          for (int j = 0; j < n; j++) {
            matrix[i][j] = scanner.nextInt();
          }
        }

    // Rotating the matrix by 90 degrees in clockwise direction
    int[][] rotatedMatrix = new int[n][n];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            rotatedMatrix[j][n - i - 1] = matrix[i][j];
        }
    }

    // Printing the rotated matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            System.out.print(rotatedMatrix[i][j] + " ");
        }
        System.out.println();
    }

    }
}
