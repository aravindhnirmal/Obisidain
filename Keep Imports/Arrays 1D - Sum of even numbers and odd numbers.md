[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc=new Scanner(System.in);
        
        int n=sc.nextInt();
        int[] arr=new int[n];
        for(int i=0;i<n;i++){
            arr[i]=sc.nextInt();
        }
        int sum1=0,sum2=0;
        for(int i=0;i<n;i++)
        {
            if(arr[i]%2==0){ // 2
                sum1=sum1+arr[i];
            }else{
                sum2=sum2+arr[i];
            }
        }
        System.out.println("The sum of the even numbers in the array is "+sum1);
        System.out.println("The sum of the odd numbers in the array is "+sum2);
    }
}

