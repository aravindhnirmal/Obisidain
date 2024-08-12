[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
         Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] house_num = new int[n];
        int[] position = new int[n];
        
        for(int i = 0; i < n; i++) {
            house_num[i] = sc.nextInt();
            position[i] = sc.nextInt();
        }
        
        int[] copy_position = new int[n];
        for(int i = 0; i < n; i++) {
            copy_position[i] = position[i];
        }
        int a;
        //Sorting 
        for(int i = 0; i < n; i++) {
            for(int j = i+1; j < n; j++) {
                if(copy_position[i] > copy_position[j]) {
                    a = copy_position[i];
                    copy_position[i] = copy_position[j];
                    copy_position[j] = a;
                }
            }
        }
        int temp;
        int x1 = 0, x2 = 0;
        int position1 = 0, position2 = 0;
        int max = 0;
        for(int i = 0; i < n - 1; i++) {
            temp = Math.abs(copy_position[i + 1] - copy_position[i]); //To Check the max diff
            if(temp > max) { /// 3 20
                max = temp;
                x1 = copy_position[i]; 
                x2 = copy_position[i + 1];
            }
        }
        for(int i = 0; i < n; i++) {
            if(x1 == position[i]) {
                position1 = i;
            } else if(x2 == position[i]) {
                position2 = i;
            }
        }
        if(house_num[position1] < house_num[position2]) {
            System.out.println(house_num[position1] + " " + house_num[position2]);
        } else {
            System.out.println(house_num[position2] + " " + house_num[position1]);
        }
    }
}

