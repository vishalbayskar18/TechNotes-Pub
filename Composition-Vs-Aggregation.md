Composition Vs Aggregation

Both are has a relation as both are subtype of association (has a relationship).

Actually it depends how you have written the code, below are 2 simple example which explain the differences.

In first if you see you are creating new object of one class (let's call it child class) inside a another class (parent class). When you implement your class like this, then whenever you delete the object of parent, 
the child references will also be deleted and this is why it is called composition (strong relation and show by filled diamond arrow).

Where as in second example, we have not created object of one class into another class, instead we have passed as argument, now both can live independently and this is why it is called aggregation 
(weaker relation and show by empty diamond arrow).

Example 1 : Composition.

```
class Engine {
 public void start() {
 System.out.println("Engine started");
 }
}
class Car {
 private Engine engine;
public Car() {
 this.engine = new Engine(); // Composition: Car "has-a" Engine
 }
public void startCar() {
 engine.start();
 }
}
public class Main {
 public static void main(String[] args) {
 Car myCar = new Car();
 myCar.startCar(); // This will start the car's engine
 }
}

```

Example 2 : Aggregation

```
class Teacher {
 private String name;
public Teacher(String name) {
 this.name = name;
 }
public void teach(Student student) {
 System.out.println(name + " is teaching " + student.getName());
 }
}
class Student {
 private String name;
public Student(String name) {
 this.name = name;
 }
public String getName() {
 return name;
 }
}
public class Main {
 public static void main(String[] args) {
 Teacher teacher = new Teacher("Mr. Smith");
 Student student = new Student("Alice");
teacher.teach(student); // Association: Teacher is associated with Student
 }
}
```
Note : The arrow direction will always be from Child to Parent, it's like soul is looking (pointing) towards the God.
