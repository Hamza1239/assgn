# assgn
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package assignment;


import static java.awt.PageAttributes.MediaType.C;
import java.io.FileReader;
import static java.lang.System.exit;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Iterator;
import java.util.List;
import java.util.Map;
import java.util.Set;
import org.json.simple.parser.JSONParser;
import org.json.simple.JSONObject;



/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

/**
 *
 * @author Hamza
 */
public class Assignment{
    String start,end,word;
    int z;

    public Assignment() {
    }
    
    public Assignment(String x)
    {
        this.word = x;
    }
    
    Assignment(String x, String y){
        start = x;        
        end = y;
        System.out.println(start);
        System.out.println(end);
    }

    
    public static void main(String[] args){
        
        List<String> path = new ArrayList<String>();
        Assignment obj = new Assignment("COLD","NODE");
        path = obj.work();   
        if(path == null)
        {
            System.out.println("Path not Found");
        }
        else{
        for(String mystr:path){
            System.out.print(mystr);
            System.out.print("-->");
        }
                    

        }
    }
    public static int getHammingDistance(String sequence1, String sequence2) {
    int a = 0;
    String sequenceX = sequence1.toLowerCase();
    String sequenceY = sequence2.toLowerCase();
    for (int x = 0; x < sequenceX.length(); x++) {
        
            if (sequenceX.charAt(x) == sequenceY.charAt(x)) {
                a += 0;
            } else if (sequenceX.charAt(x) != sequenceY.charAt(x)) {
                a += 1;
        }
    }
    return a;
}

    public static boolean exist(String x){
          loadFile obj1 = new loadFile();
          List<String> wordList = new ArrayList<String>();
          wordList = obj1.readJson("C:/Users/Hamza/Desktop/dictionary.txt");
         // System.out.println(wordList);
          for(String temp:wordList){
            if (temp.equals(x))
                return true;
                    }
          return false;
    }
    
    public List<String> output(int p){
        int counter = 0;
          loadFile obj1 = new loadFile();
          List<String> wordList = new ArrayList<String>();
          wordList = obj1.readJson("C:/Users/Hamza/Desktop/dictionary.txt");
          List<String> myList = null ;
          //wordList = obj1.getfile();
         // System.out.println("Output");
         myList= new ArrayList<String>();
          for(String temp:wordList){
             
              counter++;
//               System.out.print("Start = ");
//                System.out.println(start);
//                 System.out.print("Temp =");
//                  System.out.println(temp);
            if ((temp.length() == p) && (getHammingDistance(start,temp)==1)){
               //System.out.println("For loop");
            	   myList.add(temp);
              
                    }
          }
        //  System.out.println(counter);
          return myList;
    }
    
    public List<String> out(int p){
          loadFile obj1 = new loadFile();
          List<String> wordList = new ArrayList<String>();
          wordList = obj1.readJson("C:/Users/Hamza/Desktop/dictionary.txt");
          List<String> myList = null ;
          String abc;
          //wordList = obj1.getfile();
         // System.out.println("Output");
         abc = start;
          for(String temp:wordList){
             // System.out.println("For loop");
              myList= new ArrayList<String>();
              
            if ((temp.length() == p) && (getHammingDistance(abc,temp)==1)){
             //  System.out.println(temp);
            	   myList.add(temp);
                   abc = temp;
              
                    }
          }
          
          return myList;
    }
    
    public List<String> getsucc(String p){
          loadFile obj1 = new loadFile();
          List<String> wordList = new ArrayList<String>();
          wordList = obj1.readJson("C:/Users/Hamza/Desktop/dictionary.txt");
          List<String> myList = null ;
          int q = p.length();
          myList= new ArrayList<String>();
          for(String temp:wordList){
             // System.out.println("For loop");
              
            if ((temp.length() == q) && (getHammingDistance(p,temp)==1)){
              // System.out.println(temp);
            	   myList.add(temp);
                   p = temp;
                    }
          }
          
          return myList;
    }
    
    public int findchar(String s){   // extra function
        int counter = 0;
        for(int i = 0; i<s.length(); i++)
        {
            char x = s.charAt(i);
            char y = end.charAt(i);
             if(x == y)
               {
                  counter++;
               }
        }
      return counter;        
    } 
    
    
    
    
    public List<String> work(){    //main ftn performing all tasks
        z=getHammingDistance(start,end);
       // System.out.println("I am z:");
       // System.out.println(z);
        boolean tf1,tf2;
        tf1 = exist(start);
        tf2 = exist(end);
      //  System.out.println(tf1);
      //  System.out.println(tf2);
        if(tf1 == true && tf2 == true )
        {
           int num1 = start.length();
           int num2 = end.length();
           if(num1 == num2)
           {
               List<String> numList = new ArrayList<String>();
               List<String> currList = new ArrayList<String>();
               
               List<String> prList = new ArrayList<String>();
               List<String> lastList = new ArrayList<String>();
               numList = output(num1);
             //  System.out.println("Working");
               currList = out(num1);
               Map<String,Assignment> m1 = new HashMap();
               int x = 0, y = -1,a=0,b=0;
               
               //String temp2;
               for(String temp:numList){
                  // System.out.print("Temp = ");
                  // System.out.println(temp);
                   x = findchar(temp);
                   m1.put(temp,new Assignment(temp));
                 //  System.out.println("iN NUMLIST");
                   //if(x > y )
                   List<String> thisList = new ArrayList<String>();
                   thisList.add(start);
                   thisList.add(temp);
                       y = x;
                       prList.add(temp);
                      // System.out.print("I am in If = ");
                      // System.out.println(temp);
                       lastList = m1.get(temp).getsucc(temp);
                       for (String str:lastList)
                       {
                         
                         thisList.add(str);
                           if(str.equals(end))
                           {
                               System.out.println("Path found");
//                              
                           return thisList;
                           
                           }
                           
                       }
                   
                 //  System.out.println(x);
                  
                 //  m1.get(temp).getsucc(temp);
               }
               
               
               
               
               
               
           }
           

        }
       
        return null;
    }
}
        
    
    
    
    

