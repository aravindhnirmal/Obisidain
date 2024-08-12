[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
         Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] matrix=new int[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++)
            {
                matrix[i][j]=sc.nextInt();
            }
        }
        
        for(int i=1;i<n;i++){
            for(int j=0;j<i;j++){
                if(matrix[i][j]!=0){
                    System.out.println("Not an Upper triangular matrix");
                    return;
                }
            }
        }
        System.out.println("Upper triangular matrix");
    }
}

