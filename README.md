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

