# Guessing-Game
This program guesses user inputted number and once found determines whether number is apart of the array of numbers
/**
 * Description:
 * This program guesses user inputted number and once found determines whether number
 * is apart of the array of numbers
 * 
 * Input:
 * user input numbers are needed from user
 * 
 * Output:
 * Collection of Numbers and whether user inputted number was apart of collection
 * 
 * @author	Samuel Yohannes
 * @contact	mi8854we@go.minnstate.edu
 * @since 	09/25/23
 * 
 * Institution: Century college
 * Professor: Matthew Nyamagwa
 * 
 */


import java.util.Arrays;
import java.util.Scanner;

public class driver {

    public static void main(String[] args) {
        int[] arr = randomArray(20);
        Arrays.sort(arr);
        int target = target();
        int position = binarySearch(arr, target);

        if (position != -1) {
            System.out.println("=============================================================================\n\n"
            		+ "GREAT! Your number was found at position: =============================================================================\n\n"
            		+ "" + position + ".");
        } else {
            System.out.println("\n=============================================================================\n\n"
            		+ "SORRY! Your number is not in the collection.\n\n"
            		+ "=============================================================================");
        }

        System.out.println("Here is the Collection:");
        printArray(arr);
    }

    // Generates an array of random integers between 1 and 100 
    public static int[] randomArray(int size) {
        int[] array = new int[size];
        for (int i = 0; i < size; i++) {
            array[i] = (int) (Math.random() * 100) + 1;
        }
        return array;
    }

    // recievs target number from user
    public static int target() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Choose a random number between 1 and 100.");
        System.out.println("Enter 'Y' for Yes or 'N' for No. ");
        int target = 0;

        for (int bit = 6; bit >= 0; bit--) {
            int currentGuess = (target | (1 << bit));
            System.out.print("============\nIs your number bigger than " + currentGuess + ": ");
            char response = scanner.next().charAt(0);

            if (response == 'Y' || response == 'y') {
                target = currentGuess;
            } else {
                System.out.print("Is your number = " + currentGuess + ": ");
                response = scanner.next().charAt(0);
                if (response == 'Y' || response == 'y') {
                    return currentGuess;
                }
            }
        }
        return -1; //indicates target is not found
    }

    // Method that runs a binary search
    public static int binarySearch(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] == target) {
                return mid;
            }

            if (arr[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return -1; 
    }

    // Method to print arrays
    public static void printArray(int[] array) {
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i]);
            if (i < array.length - 1) {
                System.out.print(", ");
            }
        }
        System.out.println();
    }
}

