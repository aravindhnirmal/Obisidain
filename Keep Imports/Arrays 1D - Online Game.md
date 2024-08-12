[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc=new Scanner(System.in);
        int n=sc.nextInt();
        int[] a=new int[n];
        for(int i=0;i<n;i++){
            a[i]=sc.nextInt();
        } 
        int start=0, end=n-1;
        while(start<end)
        {
            while(a[start]%2==0 && start<end)
            {
                start++;
            }
            while(a[end]%2!=0 && start<end)
            {
                end--;
            }
            
            if(start<end)
            {
                int temp =a[start];  
                a[start]=a[end];
                a[end]=temp;
                start++;
                end--;
            }
        }
        System.out.println("Array after Segregation");
        for(int i=0;i<n;i++)
        {
            System.out.print(a[i]+" ");
        }
    }
}

