# myFirstProjectInJava.
/*TASK FIRST.
CREATE A JAVA PROGRAM TO READ, WRITE, AND MODIFY TEXT FILE.  */
//1. CREAT DEMO FILE.
package P1;

import java.io.File;
import java.io.IOException;

    public class CreateFileDemo {
        public static void main(String[] args) {
            File myFile = new File("myFile.txt");

            try{
                if(myFile.createNewFile()){
                    System.out.println("File created successfully");
                }else{
                    System.out.println("File creation failed");
                }
            }catch(IOException ex){
                System.out.println("Error creating file");
            }
        }
    }

    //2.WRITE DEMO FILE.
    
//objective of the program is the write data file.
package P1;

import java.io.FileWriter;
import java.io.IOException;

public class FileWriteDemo {
    public static void main(String[] args) {
        String data = "101,Manorama vyas,Jhalawar,Rajesthan,India";
        try {
            FileWriter obj = new FileWriter("myFile.txt");
            obj.write(data);
            System.out.println("data is written successfully");
            obj.close();
        } catch (IOException ex) {
            System.out.println("File Write Error...");
        }
    }
}

//READ DEMO FILE.

package P1;

import java.io.FileReader;

public class FileReadDemo {
    public static void main(String[] args) {
        char[]data=new char[100];
        try{
            FileReader input =new FileReader("myFile.txt");
            input.read(data);
            System.out.println("data recieved from file");
            System.out.println(data);
            input.close();
        }catch(Exception ex){
            System.out.println("File reading error");
        }
        }
    }

    //DELETE DEMO FILE.
    package P1;

import java.io.File;

public interface DeleteFileDemo {
     static void main(String[] args) {
        File myFile = new File("FileWriteDemo.mahi.class");
        if (myFile.exists()) {
            System.out.println("File Deleted:"+myFile.getName()+"successfully");
        }else{
            System.out.println("File Not Deleted:"+myFile.getName()+"failed");
        }
    }
}

//TASK 3RD.
/*JAVA MULTITHREADING BANK ATM EXAMPLE. */
// EXAMPLE 1. ACCOUNT CLASS
package p2;

public class Account {
    private int balance=6000;
    public int getBalance() {
        return balance;
    }
    public void withdraw(int amount) {
        balance -= amount;
    }
}
//CLASS ACCOUNTHOLDER

package com.infotech.worker;

import p2.Account;

public class AccountHolder  implements Runnable {
    private Account account;

    public AccountHolder(Account account) {
        this.account = account;
    }

    public void run() {
        for (int i = 0; i <= 4; i++) {
            makeWithdrawal(2000);
            if (account.getBalance() < 0) {
                System.out.println("account is overdrawn!");
            }
        }
    }
    private  void makeWithdrawal(int withdrawAmount) {
        if (account.getBalance() >= withdrawAmount) {
            System.out.println(Thread.currentThread().getName() + "  is going to withdrawn!!!" + withdrawAmount);
            try {
                Thread.sleep(3000);
            } catch (InterruptedException e) {
            }
                account.withdraw(withdrawAmount);
                System.out.println(Thread.currentThread().getName() + " completes the withdrawn of $!!!" + withdrawAmount + account.getBalance());
            }
        }
    }
    //MAIN CLASS
    package com.infotech.client;

import com.infotech.worker.AccountHolder;
import p2.Account;

public class ClientTest {
    public static void main(String[] args) {
        Account account = new Account();
        AccountHolder accountHolder = new AccountHolder(account);
        Thread t1 = new Thread(accountHolder);
        Thread t2 = new Thread(accountHolder);
        t1.start();
        t2.start();
    }
}
//EXAMPLE 2. BUS RESERVATION SYSTEM.

package bus.resevation.client;
import bus.reservation.system.TicketBookingThread;
import bus.reservation.system.TicketCounter;

public class Test {
    public static void main(String[] args) {
        TicketCounter ticketCounter=new TicketCounter();
        TicketBookingThread t1=new TicketBookingThread(ticketCounter,"John",2);
        TicketBookingThread t2=new TicketBookingThread(ticketCounter,"Martin",4);
        t1.start();
        t2.start();

    }
}
//COUNTER CLASS
package bus.reservation.system;

public class TicketCounter {
    private int availableSeats=2;
    public void bookTicket(String pname,int numOFSeats){
        if((availableSeats>=numOFSeats)&&(numOFSeats>0)){
                System.out.println("Hi  "+pname+" :"+numOFSeats+" seats booked successfully...");
                availableSeats=availableSeats-numOFSeats;
        }else{
            System.out.println("Hi  "+pname+" :"+numOFSeats+" seats not booked...");
        }
    }
}
//TICKET BOOKING THREAD.

package bus.reservation.system;

public class TicketBookingThread extends Thread {
    private final TicketCounter ticketCounter;
    private final String passengerName;
    private final int noOfSeatsToBook;
    public  TicketBookingThread(TicketCounter ticketCounter, String passengerName, int noOfSeatsToBook) {
        this.ticketCounter = ticketCounter;
        this.passengerName = passengerName;
        this.noOfSeatsToBook = noOfSeatsToBook;
    }
    public void run() {
        ticketCounter.bookTicket(passengerName, noOfSeatsToBook);
    }
    }
