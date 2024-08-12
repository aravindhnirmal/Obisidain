[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc=new Scanner(System.in);
        
        int n=sc.nextInt();
        int[] arr=new int[n];
        
        for(int i=0;i<n;i++)
        {
            arr[i]=sc.nextInt();
        }
        
        Arrays.sort(arr);
        
        int start=0,end=n-1;
        while(start<=end)
        {
            if(start==end){
                System.out.println(arr[start]+" 0");
            }else{
                System.out.println(arr[end]+" "+arr[start]);
            }
            start++;
            end--;
        }
    }
}

