[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc=new Scanner(System.in);
        int n=sc.nextInt();// 5
        int[] a1=new int[n];
        for(int i=0;i<n;i++)
        {
            a1[i]=sc.nextInt();
        }
        int count=0;
        for(int i=0;i<n;i++)
        {
            boolean isDintinct=true;
            for(int j=0;j<i;j++)
            {
                if(a1[i]==a1[j])
                {
                    isDintinct=false;
                    break;
                }
            }
            if(isDintinct)
            {
                count++;
            }
        }
        System.out.printf("There are "+count+" distinct element in the array.");
    }
}

