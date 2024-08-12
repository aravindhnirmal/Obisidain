[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

import java.util.Scanner;

public class Solution {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int fieldWidth = 15; // Width of the first column

        // Print the header line
        System.out.println("================================");

        // Read and process input lines
        while (scanner.hasNext()) {
            String s = scanner.next();
            int x = scanner.nextInt();
            String ss = scanner.next();

            // Formaat and print the line
            System.out.printf("%-" + fieldWidth + "s%03d%n", s, x);
        }

        // Print the footer line
        System.out.println("================================");
    }
}

