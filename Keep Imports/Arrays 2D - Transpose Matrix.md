[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc=new Scanner(System.in);
        
        int n=sc.nextInt();
        int[][] arr=new int[n][n];
        
        
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n;j++)
            {
                arr[i][j]=sc.nextInt();
            }
        }
        
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                System.out.print(arr[i][j]+" ");
            }
            System.out.println();
        }
        
        int[][] transpose=new int[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                transpose[j][i]=arr[i][j];// 1 4  7
                                          // 2  5 8
                                          // 3  6 9
            }
        }
        System.out.println("Transpose matrix is:");
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                System.out.print(transpose[i][j]+" ");
            }
            System.out.println();
        }
    }
}

