[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt();
        int n = sc.nextInt();
        int[][] matrix=new int[m][n];
        
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                matrix[i][j]=sc.nextInt();
            }
        }
        
        int[] maxincol=new int[n];
        
        for(int j=0;j<n;j++){
            int max=matrix[0][j];
            for(int i=0;i<m;i++){
                if(matrix[i][j]>max){
                    max=matrix[i][j];
                }
            }
            maxincol[j]=max;
        }
        
        for(int j=0;j<n;j++){
            System.out.println(maxincol[j]+" ");
        }
    }
}

