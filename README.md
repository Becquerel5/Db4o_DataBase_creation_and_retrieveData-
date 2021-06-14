# Db4o_DataBase_creation_and_retrieveData-
example is introduced in which a database of student objects is created and retrieved

STUDENT CLASS
public class Student {
int sid;
String lname;
String fname;
float gpa;
public Student(int sid, String lname, String fname, float gpa) {
this.sid = sid;
this.lname = lname;
this.fname = fname;
this.gpa = gpa;
}
public int getSid() {
return sid;
}
public void setSid(int sid) {
this.sid = sid;
}
public String getLname() {
return lname;
}
public void setLname(String lname) {
this.lname = lname;
}
public String getFname() {
return fname;
}
public void setFname(String fname) {
this.fname = fname;
}
public float getGpa() {

return gpa;
}
public void setGpa(float gpa) {
this.gpa = gpa;
}
public String toString() {
return sid+" "+fname+" "+lname;
}
}

CREATE STUDENT CLASS

import com.db4o.Db4o;
import com.db4o.ObjectContainer;
import com.db4o.config.Configuration;
public class CreateStudent {
public static void main(String[] args) {
Configuration config = Db4o.configure();
ObjectContainer db = Db4o.openFile(config,"student.db4o");
createFewStudents(db);
db.close();
}
public static void createFewStudents(ObjectContainer db) {
//Create few student objects and store them in the database
Student s1 = new Student(1000,"Smith","Josh", (float) 3.00);
Student s2 = new Student(1001,"Harvey", "Derek", (float) 4.00);
Student s3 = new Student(1002,"Lemon", "Don", (float) 3.50);
db.store(s1);
db.store(s2);
db.store(s3);
}
}

FINALLY PRINT STUDENT CLASS
import com.db4o.Db4o;
import com.db4o.ObjectContainer;
import com.db4o.ObjectSet;

import com.db4o.config.Configuration;
public class PrintStudents {
public static void main(String[] args) {
Configuration config = Db4o.configure();
ObjectContainer db = Db4o.openFile(config,"student.db4o");
printStudents(db);
db.close();
}
public static void printStudents(ObjectContainer db) {
ObjectSet result = db.queryByExample(Student.class);
System.out.println("Number of students: " + result.size()+"\n");
while (result.hasNext()) {
Student s = (Student) result.next();
System.out.println(s);
}
}
}

