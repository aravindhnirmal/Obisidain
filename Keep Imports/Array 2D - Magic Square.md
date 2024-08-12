[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
           Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[][] a = new int[n][n];
        int d1 = 0, d2 = 0;
        
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                a[i][j] = sc.nextInt();
            }
        }
        
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++)
            {
                if(i == j){           //find forward sum 1+6+11+16
                    d1 += a[i][j];
                }
                if(i == n - j - 1){   // find backward sum 4+7+10+13
                    d2 += a[i][j];
                }
            }
        }
            
        if(d1 == d2){
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
}

