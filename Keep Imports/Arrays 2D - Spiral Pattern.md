[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

 import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[][] matrix = new int[n][n];

        // Reading the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }
        
        for (int i = 0; i < (n + 1) / 2; i++){
            for(int j=i;j<=n-i-1;j++) //Traverse from left to right
            {
                System.out.print(matrix[i][j] + " ");
            }
            
            for(int j=i+1;j<=n-i-1;j++) //Traverse from top to bottom
            {
                System.out.print(matrix[j][n-i-1] + " ");
            }
            
            for(int j=n-i-2;j>=i;j--) //Traverse from right to left
            {
                System.out.print(matrix[n-i-1][j] + " ");
            }
            
            for(int j=n-i-2;j>i;j--) //Traverse from bottom to right
            {
                System.out.print(matrix[j][i] + " ");
            }
        }
    }
}

