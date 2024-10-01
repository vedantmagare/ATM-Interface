# ATM-Interface
package InternshipProject;

import java.util.ArrayList;
import java.util.Scanner;

public class ATM {

	private static Scanner scanner = new Scanner(System.in);
	private static ArrayList<String> transactionHistory = new ArrayList<>();
	private static double balance = 0.0;
	private static int userId = 12345;
	private static int userPin = 1234;

	public static void main(String[] args) {
		if (authenticateUser()) {
			showMenu();
		} else {
			System.out.println("Invalid User ID or PIN. Exiting...");
		}
	}

	// Function to authenticate the user
	private static boolean authenticateUser() {
		System.out.print("Enter User ID: ");
		int inputUserId = scanner.nextInt();
		System.out.print("Enter User PIN: ");
		int inputUserPin = scanner.nextInt();

		return inputUserId == userId && inputUserPin == userPin;
	}

	// Function to display the main menu
	private static void showMenu() {
		int choice;
		do {
			System.out.println("\nWelcome to the ATM System");
			System.out.println("1. Transaction History");
			System.out.println("2. Withdraw");
			System.out.println("3. Deposit");
			System.out.println("4. Transfer");
			System.out.println("5. Quit");
			System.out.print("Choose an option: ");
			choice = scanner.nextInt();

			switch (choice) {
			case 1:
				showTransactionHistory();
				break;
			case 2:
				withdraw();
				break;
			case 3:
				deposit();
				break;
			case 4:
				transfer();
				break;
			case 5:
				System.out.println("Thank you for using the ATM. Goodbye!");
				break;
			default:
				System.out.println("Invalid option. Please choose again.");
			}
		} while (choice != 5);
	}

	// Function to display transaction history
	private static void showTransactionHistory() {
		if (transactionHistory.isEmpty()) {
			System.out.println("No transactions yet.");
		} else {
			System.out.println("Transaction History:");
			for (String transaction : transactionHistory) {
				System.out.println(transaction);
			}
		}
	}

	// Function to withdraw money
	private static void withdraw() {
		System.out.print("Enter the amount to withdraw: ");
		double amount = scanner.nextDouble();
		if (amount > 0 && amount <= balance) {
			balance -= amount;
			transactionHistory.add("Withdrawn: $" + amount);
			System.out.println("Withdrawal successful. New balance: $" + balance);
		} else {
			System.out.println("Insufficient balance or invalid amount.");
		}
	}

	// Function to deposit money
	private static void deposit() {
		System.out.print("Enter the amount to deposit: ");
		double amount = scanner.nextDouble();
		if (amount > 0) {
			balance += amount;
			transactionHistory.add("Deposited: $" + amount);
			System.out.println("Deposit successful. New balance: $" + balance);
		} else {
			System.out.println("Invalid deposit amount.");
		}
	}

	// Function to transfer money
	private static void transfer() {
		System.out.print("Enter the recipient's User ID: ");
		int recipientId = scanner.nextInt();
		System.out.print("Enter the amount to transfer: ");
		double amount = scanner.nextDouble();
		if (amount > 0 && amount <= balance) {
			balance -= amount;
			transactionHistory.add("Transferred: $" + amount + " to User ID " + recipientId);
			System.out.println("Transfer successful. New balance: $" + balance);
		} else {
			System.out.println("Insufficient balance or invalid amount.");
		}
	}
}
