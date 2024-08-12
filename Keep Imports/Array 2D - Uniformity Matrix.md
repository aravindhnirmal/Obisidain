[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc=new Scanner(System.in);
        
        int n=sc.nextInt();
        int[][] a=new int[n][n];
        
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                a[i][j]=sc.nextInt();
            }
        }
        int ocount=0,ecount=0;
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                if(a[i][j]%2==0){
                    ecount++;
                }
                else{
                    ocount++;
                }
            }
        }
        if(ecount==(n*n)|| ocount==(n*n)){
            System.out.println("Yes");
        }else{
            System.out.println("No");
        }
    }
}

