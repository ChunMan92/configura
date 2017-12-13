# configura
Configura Programming Challenge
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package copyfile;

/**
 *
 * @author Ah Man
 * 
 */
import java.io.*;
import java.util.*;
public class CopyFile {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        File file = new File("C:\\Users\\Chun\\Documents\\NetBeansProjects\\CopyFile\\test.txt");
        File copyfile = new File("C:\\Users\\Chun\\Documents\\NetBeansProjects\\test.txt");
        BufferedReader reader;
        PrintWriter writer;
        String line;
        
        try {
            if (copyfile.createNewFile() || !copyfile.createNewFile()){
                reader = new BufferedReader(new FileReader(file));
                writer = new PrintWriter(new FileWriter(copyfile));
                
                while ((line = reader.readLine()) != null){
                    writer.println(line);
                    
                }
                System.out.println("The file is backuped successfully in C:\\Users\\Chun\\Documents\\NetBeansProjects\\test.txt .");
                reader.close();
                writer.close();
            }
        } catch (IOException ioEx) {
            System.err.println("Error, The file is not exists");
            
        }
    }
    
}
