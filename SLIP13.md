Question A: Java Program for Thread Name in Multithreading
Solution:
// MyThread.java
class MyThread extends Thread {
    public MyThread(String name) {
        super(name);
    }

    @Override
    public void run() {
        System.out.println("Thread Name: " + Thread.currentThread().getName());
    }
}

public class ThreadName {
    public static void main(String[] args) {
        MyThread thread1 = new MyThread("FirstThread");
        MyThread thread2 = new MyThread("SecondThread");
        thread1.start();
        thread2.start();
        System.out.println("Thread Name from Main: " + Thread.currentThread().getName()); // Main thread name
    }
}

Question B: JSP Program to Display College Details in Tabular Form
Solution:
<%-- CollegeDetails.jsp --%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>College Details</title>
</head>
<body>
    <h2>College Details</h2>
    <table border="1">
        <tr>
            <th>College ID</th>
            <th>College Name</th>
            <th>Address</th>
        </tr>
        <tr>
            <td>101</td>
            <td>ABC College</td>
            <td>City X</td>
        </tr>
        <tr>
            <td>102</td>
            <td>XYZ University</td>
            <td>City Y</td>
        </tr>
        <tr>
            <td>103</td>
            <td>PQR Institute</td>
            <td>City Z</td>
        </tr>
    </table>
</body>
</html>

Question A: VB.net Program for Blinking Image
Public Class Form1

    Private isImageVisible As Boolean = True ' To track image visibility

    Private Sub timerBlink_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles timerBlink.Tick
        If isImageVisible Then
            pictureBoxImage.Visible = False ' Hide the image
        Else
            pictureBoxImage.Visible = True  ' Show the image
        End If
        isImageVisible = Not isImageVisible ' Toggle the visibility state
    End Sub
End Class

Question B: C# Program to Accept and Display Student Details

using System;

namespace StudentDetailsApp
{
    // Define a class to represent a Student
    class Student
    {
        public int RollNo { get; set; }
        public string Name { get; set; }
        public double Subject1Marks { get; set; }
        public double Subject2Marks { get; set; }
        public double Subject3Marks { get; set; }

        // Method to calculate percentage
        public double CalculatePercentage()
        {
            return (Subject1Marks + Subject2Marks + Subject3Marks) / 3.0;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Enter the number of students: ");
            int n = int.Parse(Console.ReadLine());

            Student[] students = new Student[n]; // Array to hold student objects

            for (int i = 0; i < n; i++)
            {
                Console.WriteLine($"\nEnter details for student {i + 1}:");
                Student student = new Student();

                Console.Write("Roll No: ");
                student.RollNo = int.Parse(Console.ReadLine());

                Console.Write("Name: ");
                student.Name = Console.ReadLine();

                Console.Write("Marks in Subject 1: ");
                student.Subject1Marks = double.Parse(Console.ReadLine());

                Console.Write("Marks in Subject 2: ");
                student.Subject2Marks = double.Parse(Console.ReadLine());

                Console.Write("Marks in Subject 3: ");
                student.Subject3Marks = double.Parse(Console.ReadLine());

                students[i] = student; // Store the student object in the array
            }

            Console.WriteLine("\nStudent Details:");
            Console.WriteLine("---------------------------------------------------");
            Console.WriteLine("Roll No\tName\tSub1\tSub2\tSub3\tPercentage");
            Console.WriteLine("---------------------------------------------------");

            foreach (var student in students)
            {
                double percentage = student.CalculatePercentage();
                Console.WriteLine($"{student.RollNo}\t{student.Name}\t{student.Subject1Marks}\t{student.Subject2Marks}\t{student.Subject3Marks}\t{percentage:F2}%"); // :F2 to format percentage to 2 decimal places
            }

            Console.ReadKey(); // Keep console window open until a key is pressed
        }
    }
}
