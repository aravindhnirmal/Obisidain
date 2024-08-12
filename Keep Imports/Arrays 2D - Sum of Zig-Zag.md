[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 


import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
          Scanner sc=new Scanner(System.in);
        
        int row=sc.nextInt();
        int col=sc.nextInt();
        int[][] arr=new int[row][col];
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                arr[i][j]=sc.nextInt();
            }
        }
        
        int total=0;
        for(int i=0;i<row;i++){
            for(int j=0;j<col;j++){
                if(i==0||i==row-1||i+j==row-1){
                    total+=arr[i][j];
                }
            }
        }System.out.println("Sum of Zig-Zag pattern is "+total);
    }
}
