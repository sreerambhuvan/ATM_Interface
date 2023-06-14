# ATM_Interface


import java.util.Scanner;

class Bank {

    String name;
    String userName;
    String password;
    String accountNo;
    float balance = 100000f;
    int transactions = 0;
    String transactionHistory = "";



    public void register() {
        Scanner sc = new Scanner(System.in);
        System.out.print("\nEnter Your Name - ");
        this.name = sc.nextLine();
        System.out.print("\nEnter Your Username - ");
        this.userName = sc.nextLine();
        System.out.print("\nPassword Generation:\n Password should be more than 6 Characters  and should not be same as username!!(for your security)\n Kindly Cooperate with us \nEnter Your password-- ");

        this.password = sc.nextLine();
        while(password.length()<=6||password.equals(userName)){
            System.out.print("Please follow the instructions and kinly change your password-");
            this.password=sc.nextLine();
        }

        System.out.print("\nEnter Your Account Number - ");
        this.accountNo = sc.nextLine();
        System.out.println("\nRegistration completed..kindly login");
    }

    public boolean login() {
        boolean isLogin = false;
        Scanner sc = new Scanner(System.in);
        while ( !isLogin ) {
            System.out.print("\nEnter Your Username - ");
            String Username = sc.nextLine();
            if ( Username.equals(userName) ) {
                while ( !isLogin ) {
                    System.out.print("\n1.Enter Your Password");
                    System.out.print("\n2.forgot password");
                    System.out.print("\nPlease select an option--");
                    int  num=sc.nextInt();
                    if(num==1){
                        System.out.print("\nKindly enter the password--");

                        String Password = sc.next();
                        if ( Password.equals(password) ) {
                            System.out.println("\nLogin successful!!");
                            isLogin = true;
                        }
                        else {
                            System.out.println("\nIncorrect Password");
                        }
                    }
                    else if(num==2){
                        System.out.print("\n To recover your password,please enter your account Number--");

                        String n=sc.next();
                        if(n.equals(accountNo)){
                            System.out.print("\n Please enter the new password-");

                            String p1=sc.next();
                            System.out.print("\n Please renter to confirm-");

                            String p2=sc.next();
                            if(p1.equals(p2)){
                                password=p1;
                                System.out.print("\n-----Your password updated Successfully Kindly Login again-----");
                            }
                            else{
                                System.out.print("\npasswords doesn't match..");
                                System.out.println();

                            }
                        }
                        else{
                            System.out.print("\nAccount Number is incorrect");
                        }
                    }
                    else{
                        System.out.print("\nPlease enter valid number");
                    }
                }
            }
            else {
                System.out.println("\nUsername not found");
            }
        }
        return isLogin;
    }

    public void withdraw() {

        System.out.print("\nEnter amount to withdraw - ");
        Scanner sc = new Scanner(System.in);
        float amount = sc.nextFloat();
        try {

            if ( balance >= amount ) {
                transactions++;
                balance -= amount;
                System.out.println("\nWithdraw Successfully");
                String str = amount + " Rs Withdrawed\n";
                transactionHistory = transactionHistory.concat(str);

            }
            else {
                System.out.println("\nInsufficient Balance");
            }

        }
        catch ( Exception e) {
        }
    }

    public void deposit() {

        System.out.print("\nEnter amount to deposit - ");
        Scanner sc = new Scanner(System.in);
        float amount = sc.nextFloat();

        try {
            if ( amount <= 100000f ) {
                transactions++;
                balance += amount;
                System.out.println("\nThank You ..Successfully Deposited");
                String str = amount + " Rs deposited\n";
                transactionHistory = transactionHistory.concat(str);
            }
            else {
                System.out.println("\nSorry:) Limit is 100000.00");
            }

        }
        catch ( Exception e) {
        }
    }

    public void transfer() {

        Scanner sc = new Scanner(System.in);
        System.out.print("\nEnter Receipent's Name - ");
        String receipent = sc.nextLine();
        System.out.print("\nEnter amount to transfer - ");
        float amount = sc.nextFloat();

        try {
            if ( balance >= amount ) {
                if ( amount <= 50000f ) {
                    transactions++;
                    balance -= amount;
                    System.out.println("\nSuccessfully Transfered to " + receipent);
                    String str = amount + " Rs transfered to " + receipent + "\n";
                    transactionHistory = transactionHistory.concat(str);
                }
                else {
                    System.out.println("\nSorry Max Transfer Amount is 50000.00");
                }
            }
            else {
                System.out.println("\nInsufficient Balance");
            }
        }
        catch ( Exception e) {
        }
    }

    public void checkBalance() {
        System.out.println("\nYour Account Balance is: " + balance + " Rs");
    }

    public void transHistory() {
        if ( transactions == 0 ) {
            System.out.println("\nEmpty");
        }
        else {
            System.out.println("\n" + transactionHistory);
        }
    }
}


public class cp {


    public static int takeIntegerInput(int limit) {
        int input = 0;
        boolean flag = false;

        while ( !flag ) {
            try {
                Scanner sc = new Scanner(System.in);
                input = sc.nextInt();
                flag = true;

                if ( flag && input > limit || input < 1 ) {
                    System.out.println("Choose the number between 1 to " + limit);
                    flag = false;
                }
            }
            catch ( Exception e ) {
                System.out.println("Enter only integer value");
                flag = false;
            }
        };
        return input;
    }


    public static void main(String[] args) {

        System.out.println("\n---------WELCOME :)---------\n");
        System.out.println("1.Register for New Account \n2.Exit");
        System.out.print("Enter Your Choice-");
        int choice = takeIntegerInput(2);

        if ( choice == 1 ) {
            Bank b = new Bank();
            b.register();
            while(true) {
                System.out.println("\n1.Login into Savings Account \n2.Exit");
                System.out.print("Enter Your Choice-");
                int ch = takeIntegerInput(2);
                if ( ch == 1 ) {
                    if (b.login()) {
                        System.out.println("\n\n**********Welcome" + (b.name).toUpperCase() + " **********\n");
                        boolean isFinished = false;
                        while (!isFinished) {
                            System.out.println("\n1.Transaction History \n2.Withdraw \n3.Deposit\n4.Transfer\n5.Balance Enquiry \n6.Exit");
                            System.out.print("\nEnter Your Choice - ");
                            int c = takeIntegerInput(6);
                            switch(c) {
                                case 2:
                                    b.withdraw();
                                    break;
                                case 3:
                                    b.deposit();
                                    break;
                                case 4:
                                    b.transfer();
                                    break;
                                case 5:
                                    b.checkBalance();
                                    break;
                                case 1:
                                    b.transHistory();
                                    break;
                                case 6:
                                    isFinished = true;
                                    break;
                            }
                        }
                    }
                }
                else {
                    System.exit(0);
                }
            }
        }
        else {
            System.exit(0);
        }



    }
}
