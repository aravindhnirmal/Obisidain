[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution.*/
        Scanner sc=new Scanner(System.in);
        int n=sc.nextInt();
        int m=sc.nextInt();
        int[] a=new int[n];
        for(int i=0;i<n;i++){
            a[i]=sc.nextInt();
        } 
        int buses=0;
        int people=0;
        for(int i=0;i<n;i++)
        {
            if(people+a[i]<=m)
            {
                people=people+a[i];
            }else{
                buses++;
                people=a[i];
            }
        }
        if(people>0){
            buses++;
        }
        System.out.println(buses);
    }
}

