[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.util.ArrayList;

public class ArrayListAndArrayExample {
    public static void main(String[] args) {
        ArrayList<Integer> al = new ArrayList<Integer>();
        al.add(12);
        al.add(10);

        int[] arr = {1, 2, 2, 33, 2, 3, 4, 252, 5, 25, 2};

        for (int is = 0; is < arr.length; is++) {
            System.out.println(arr[is]); // Access and print individual elements
        }

        for (int i = 0; i < al.size(); i++) {
            System.out.println(al.get(i));
        }
    }
}

