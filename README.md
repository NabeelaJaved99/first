# first
import java.util.Scanner; // Import the Scanner class to read user input

public class LineCoding {
    
    // Method for Unipolar NRZ Encoding
    // In Unipolar NRZ, '1' is represented by a high signal and '0' by a low (zero) signal.
    static void unipolarNRZ(int[] data) {
        System.out.println("Unipolar NRZ Encoding:");
        // Loop through the data bits
        for (int bit : data) {
            // Print high signal for '1' and low signal for '0'
            if (bit == 1) System.out.print("|‾| ");   // High signal for '1'
            else System.out.print("|__| ");          // Low signal for '0'
        }
        System.out.println(); // Move to the next line after printing all bits
    }

    // Method for Polar NRZ Encoding
    // In Polar NRZ, '1' is represented by a positive voltage and '0' by a negative voltage.
    static void polarNRZ(int[] data) {
        System.out.println("Polar NRZ Encoding:");
        // Loop through the data bits
        for (int bit : data) {
            // Print positive signal for '1' and negative signal for '0'
            if (bit == 1) System.out.print("|‾| ");  // Positive signal for '1'
            else System.out.print("|__| ");         // Negative signal for '0'
        }
        System.out.println(); // Move to the next line after printing all bits
    }

    // Method for Manchester Encoding
    // In Manchester Encoding, each bit has a transition in the middle of the bit period.
    // '1' is represented by a transition from low to high, and '0' by a transition from high to low.
    static void manchester(int[] data) {
        System.out.println("Manchester Encoding:");
        // Loop through the data bits
        for (int bit : data) {
            // Print transition for '1' and '0'
            if (bit == 1) System.out.print("|__‾| ");  // Transition from low to high for '1'
            else System.out.print("|‾__| ");         // Transition from high to low for '0'
        }
        System.out.println(); // Move to the next line after printing all bits
    }

    // Method for Differential Manchester Encoding
    // In Differential Manchester Encoding, there is always a transition in the middle of the bit.
    // '1' is represented by a transition at the start of the bit period, and '0' by no transition at the start.
    static void differentialManchester(int[] data) {
        System.out.println("Differential Manchester Encoding:");
        int lastTransition = 1; // Assume initial transition starts as high
        // Loop through the data bits
        for (int bit : data) {
            if (bit == 0) {
                // If bit is '0', no transition at the start of the bit period
                if (lastTransition == 1) System.out.print("|__‾| ");  // No transition, stay at low to high
                else System.out.print("|‾__| ");                     // No transition, stay at high to low
                lastTransition = -lastTransition; // Toggle the last transition state
            } else {
                // If bit is '1', transition at the start of the bit period
                if (lastTransition == 1) System.out.print("|‾__| ");  // Transition from high to low for '1'
                else System.out.print("|__‾| ");                     // Transition from low to high for '1'
                lastTransition = -lastTransition; // Toggle the last transition state
            }
        }
        System.out.println(); // Move to the next line after printing all bits
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in); // Create a Scanner object for input
        
        // Ask the user for the number of bits in the data
        System.out.println("Enter the number of bits in the data:");
        int n = sc.nextInt(); // Read the number of bits
        int[] data = new int[n]; // Create an array to hold the data bits

        // Ask the user to input the binary data bits (0s and 1s)
        System.out.println("Enter the binary data bits (0s and 1s):");
        for (int i = 0; i < n; i++) {
            data[i] = sc.nextInt(); // Read each bit and store it in the array
        }

        // Perform line coding techniques on the input data
        unipolarNRZ(data);            // Call Unipolar NRZ encoding method
        polarNRZ(data);               // Call Polar NRZ encoding method
        manchester(data);              // Call Manchester encoding method
        differentialManchester(data);  // Call Differential Manchester encoding method
        
        sc.close(); // Close the Scanner object to prevent resource leakage
    }
}
