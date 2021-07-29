- 👋 Hi, I’m @ap33724
- 👀 This file contains interview questions with answers on Java
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
ap33724/ap33724 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

Q1-What is marker interface?
A- Any interface which do not have any method is called marker interface.

Q2-What is the use of marker interface?
A-The whole idea of Marker Interface Pattern is to provide a mean to say "yes I am something" and then system will proceed with the default process, 
like when you mark your class as Serialzable it just tells that this class can be converted to bytes.

Q3-Exampler of marker interface?
A-Create the empty interface
interface Marker{    }
Write a class and implements the interface

class A implements Marker {
    //do some task
}
Main class to check the marker interface instanceof
class Main {
    public static void main(String[] args) {
        A ob = new A(){
        if (ob instanceof A) {
            // do some task
        }
    }
}

Q4- Why string is immutable?
A-The string is Immutable in Java because String objects are cached in the String pool. 
Since cached String literals are shared between multiple clients there is always a risk, where one client's action would affect all another client.
For example, if one client changes the value of the String "Test" to "TEST", all other clients will also see that value as explained in the first example. 
Since caching of String objects was important from performance reason this risk was avoided by making String class Immutable. 
At the same time, String was made final so that no one can compromise invariant of String class like Immutability, 
Caching, hashcode calculation, etc by extending and overriding behaviors.
Another reason why String class is immutable could die due to HashMap.

Q5- How to make immutable class?
A-Immutable objects are instances whose state doesn’t change after it has been initialized.Used in case of caching & thread-safety.

Steps:
-------------------------------------------------------------------------------------------------
The class must be declared as final (So that child classes can’t be created)
Data members in the class must be declared as private (So that direct access is not allowed)
Data members in the class must be declared as final (So that we can’t change the value of it after object creation)
A parameterized constructor should initialize all the fields performing a deep copy (So that data members can’t be modified with object reference)
Deep Copy of objects should be performed in the getter methods (To return a copy rather than returning the actual object reference)
No setters (To not have the option to change the value of the instance variable)
-------------------------------------------------------------------------------------------------
import java.util.HashMap;
import java.util.Map;
 
// An immutable class
public final class Student {
    private final String name;
    private final int regNo;
    private final Map<String, String> metadata;
 
    public Student(String name, int regNo,
                   Map<String, String> metadata)
    {
        this.name = name;
        this.regNo = regNo;
        Map<String, String> tempMap = new HashMap<>();
        for (Map.Entry<String, String> entry :
             metadata.entrySet()) {
            tempMap.put(entry.getKey(), entry.getValue());
        }
        this.metadata = tempMap;
    }
 
    public String getName() { return name; }
 
    public int getRegNo() { return regNo; }
 
    public Map<String, String> getMetadata()
    {
        Map<String, String> tempMap = new HashMap<>();
        for (Map.Entry<String, String> entry :
             this.metadata.entrySet()) {
            tempMap.put(entry.getKey(), entry.getValue());
        }
        return tempMap;
    }
}
