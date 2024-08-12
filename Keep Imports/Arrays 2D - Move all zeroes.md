[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc=new Scanner(System.in);
        int t=sc.nextInt();
        
        while(t-- > 0)
        {
            int r,count=0,ans=0;
            int num=sc.nextInt();
            while(num!=0)
            {
                r=num%10;
                if(r==0){
                    count++; //Find the no of 0's
                }
                else{
                    ans=(ans*10)+r; // TO get the no of 1
                }
                num=num/10;
            }
            System.out.print(ans);
            for(int i=0;i<count;i++){
                System.out.print("0");
            }
            System.out.println();
        }
    }
}

