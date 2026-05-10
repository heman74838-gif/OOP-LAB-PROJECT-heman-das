# OOP-LAB-PROJECT-heman-das
import java.util.Scanner;
// PROCEDURAL APPROACH

class ATMProcedural {

    static double balance = 10000;
    static int pin = 1234;

    static boolean verifyPin(int enteredPin) {
        return enteredPin == pin;
    }

    static void checkBalance() {
        System.out.println("Procedural Balance: " + balance);
    }

    static void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposit Successful!");
        } else {
            System.out.println("Invalid amount!");
        }
    }

    static void withdraw(double amount) {
        if (amount > balance) {
            System.out.println("Insufficient Balance!");
        } else {
            balance -= amount;
            System.out.println("Withdraw Successful!");
        }
    }
}
// OOP APPROACH
class ATM {

    // Encapsulation
    private double balance;
    private int pin;

    // Constructor
    public ATM(double balance, int pin) {
        this.balance = balance;
        this.pin = pin;
    }

    // Verify PIN
    public boolean verifyPin(int enteredPin) {
        return enteredPin == pin;
    }

    // Check Balance
    public void checkBalance() {
        System.out.println("Current Balance: " + balance);
    }

    // Deposit
    public void deposit(double amount) {

        if (amount > 0) {
            balance += amount;

            System.out.println("Deposit Successful!");
            System.out.println("Updated Balance: " + balance);

        } else {
            System.out.println("Invalid Amount!");
        }
    }

    // Withdraw
    public void withdraw(double amount) {

        if (amount > balance) {

            System.out.println("Insufficient Balance!");

        } else if (amount <= 0) {

            System.out.println("Invalid Amount!");

        } else {

            balance -= amount;

            System.out.println("Withdraw Successful!");
            System.out.println("Remaining Balance: " + balance);
        }
    }
}

// INHERITANCE

class Account {

    protected double balance;

    public Account(double balance) {
        this.balance = balance;
    }
}

class SavingsAccount extends Account {

    public SavingsAccount(double balance) {
        super(balance);
    }

    public void showType() {
        System.out.println("Savings Account Created");
    }
}

// MAIN CLASS

public class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

     
        // PROCEDURAL DEMO
       

        System.out.println(" PROCEDURAL APPROACH ");

        if (ATMProcedural.verifyPin(1234)) {

            ATMProcedural.checkBalance();
            ATMProcedural.deposit(2000);
            ATMProcedural.withdraw(1000);
        }

        // OOP DEMO

        System.out.println("\n OBJECT ORIENTED APPROACH ");

        // Object Creation
        ATM atm = new ATM(10000, 1234);

        // Inheritance Object
        SavingsAccount acc = new SavingsAccount(10000);
        acc.showType();

        System.out.print("Enter PIN: ");
        int enteredPin = sc.nextInt();

        if (!atm.verifyPin(enteredPin)) {

            System.out.println("Wrong PIN!");
            return;
        }

        int choice;

        do {

            System.out.println("\n===== ATM MENU =====");
            System.out.println("1. Check Balance");
            System.out.println("2. Deposit");
            System.out.println("3. Withdraw");
            System.out.println("4. Exit");

            System.out.print("Enter choice: ");
            choice = sc.nextInt();

            switch (choice) {

                case 1:

                    atm.checkBalance();
                    break;

                case 2:

                    System.out.print("Enter deposit amount: ");
                    double dep = sc.nextDouble();

                    atm.deposit(dep);
                    break;

                case 3:

                    System.out.print("Enter withdraw amount: ");
                    double wd = sc.nextDouble();

                    atm.withdraw(wd);
                    break;

                case 4:

                    System.out.println("Thank you for using ATM!");
                    break;

                default:

                    System.out.println("Invalid choice!");
            }

        } while (choice != 4);

        sc.close();
    }
}
