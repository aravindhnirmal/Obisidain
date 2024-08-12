[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 


import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
         Scanner sc=new Scanner(System.in);
        int m=sc.nextInt();
        int n=sc.nextInt();
        
        int[][] a=new int[m][n];
        int[][] b=new int[m][n];
        
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                a[i][j]=sc.nextInt();
            }
        }
        
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                b[i][j]=sc.nextInt();
            }
        }
        
        int[][] c=new int[m][n];
        
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                for(int k=0;k<m;k++){
                    c[i][j]= c[i][j]+a[i][k]*b[k][j];
                }
            }
        }
        
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                System.out.print(c[i][j]+" ");
            }
            System.out.println();
        }
    }
}
