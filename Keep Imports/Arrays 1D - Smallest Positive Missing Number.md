[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] a = new int[n];
        for (int i = 0; i < n; i++) {
           a[i] = sc.nextInt();
        }
        //sc.close();
        Arrays.sort(a);
        int missing = 1;
        for (int i = 0; i < n; i++) {
        if (a[i] <= 0)
            continue;
        if (a[i] == missing)
        {
            missing++;
        } 
        else if (a[i] > missing)
        {
           break;
        }
        }
        System.out.println(missing);
        }
        }

