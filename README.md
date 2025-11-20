# codealpha_tasks #
Task 1 Solution [Java Programming]
import java.util.ArrayList;
import java.util.Scanner;

class Student {
    String name;
    double grade;

    Student(String name, double grade) {
        this.name = name;
        this.grade = grade;
    }
}

public class StudentGradeTracker {

    private static final ArrayList<Student> students = new ArrayList<>();
    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {

        while (true) {
            System.out.println("\n===== STUDENT GRADE TRACKER =====");
            System.out.println("1. Add Student");
            System.out.println("2. Show All Students");
            System.out.println("3. Show Average Grade");
            System.out.println("4. Show Highest Grade");
            System.out.println("5. Show Lowest Grade");
            System.out.println("6. Exit");
            System.out.print("Choose an option: ");

            int choice = getIntInput();

            switch (choice) {
                case 1 -> addStudent();
                case 2 -> showAllStudents();
                case 3 -> showAverage();
                case 4 -> showHighest();
                case 5 -> showLowest();
                case 6 -> {
                    System.out.println("Exiting... Goodbye!");
                    return;
                }
                default -> System.out.println("Invalid option. Try again.");
            }
        }
    }
    private static int getIntInput() {
        while (!scanner.hasNextInt()) {
            System.out.print("Invalid input. Enter a number: ");
            scanner.next();
        }
        return scanner.nextInt();
    }

    private static void addStudent() {
        scanner.nextLine();
        System.out.print("Enter student name: ");
        String name = scanner.nextLine();

        System.out.print("Enter grade: ");
        double grade = getValidDouble();

        students.add(new Student(name, grade));
        System.out.println("✔ Student added successfully.");
    }
getValidDouble() {
        while (!scanner.hasNextDouble()) {
            System.out.print("Invalid grade. Enter a number: ");
            scanner.next();
        }
        return scanner.nextDouble();
    }

    private static void showAllStudents() {
        if (students.isEmpty()) {
            System.out.println("No students added yet.");
            return;
        }
        System.out.println("\n===== STUDENT SUMMARY =====");
        for (Student s : students) {
            System.out.println(s.name + " -> " + s.grade);
        }
    }

    private static void showAverage() {
        if (students.isEmpty()) {
            System.out.println("No data available.");
            return;
        }

        double sum = 0;
        for (Student s : students) sum += s.grade;

        double avg = sum / students.size();
        System.out.println("Average Grade: " + avg);
    }

    private static void showHighest() {
        if (students.isEmpty()) {
            System.out.println("No data available.");
            return;
        }

        Student top = students.get(0);
        for (Student s : students) {
            if (s.grade > top.grade) top = s;
        }

        System.out.println("Highest Grade: " + top.grade + " (" + top.name + ")");
    }

    private static void showLowest() {
        if (students.isEmpty()) {
            System.out.println("No data available.");
            return;
        }

        Student low = students.get(0);
        for (Student s : students) {
            if (s.grade < low.grade) low = s;
        }

        System.out.println("Lowest Grade: " + low.grade + " (" + low.name + ")");
    }
}
