Q.1. A) Write a java program to calculate factorial of a number. (Use sleep () method).
Java Program (FactorialSleep.java):
import java.util.Scanner;

public class FactorialSleep {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a non-negative integer: ");
        int number = scanner.nextInt();

        if (number < 0) {
            System.out.println("Factorial is not defined for negative numbers.");
            return;
        }

        long factorial = 1;
        System.out.println("Calculating factorial of " + number + "...");

        for (int i = 1; i <= number; i++) {
            factorial *= i;
            System.out.println("Step " + i + ": Current Factorial = " + factorial);
            try {
                Thread.sleep(500); // Pause for 0.5 seconds to demonstrate sleep()
            } catch (InterruptedException e) {
                System.out.println("Thread sleep interrupted!");
            }
        }

        System.out.println("\nFactorial of " + number + " = " + factorial);
        scanner.close();
    }
}

Q.1. B) Write a java program for simple standalone chatting application.
Java Program (SimpleChat.java):
import java.util.Scanner;

public class SimpleChat {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Simple Chat Application Started!");
        System.out.println("Type 'bye' to exit.");

        while (true) {
            System.out.print("You: ");
            String message = scanner.nextLine();

            if (message.equalsIgnoreCase("bye")) {
                System.out.println("ChatBot: Goodbye!");
                break; // Exit the loop and end chat
            }

            System.out.println("ChatBot: You said: " + message); // Simple echo as chatbot response
        }
        scanner.close();
        System.out.println("Chat Application Ended.");
    }
}
