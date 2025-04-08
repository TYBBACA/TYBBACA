A) Write a JSP program to accept Name and Age of Voter and check whether he is eligible for voting or not.
JSP Code (voting_check.jsp):
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>Voting Eligibility Checker</title>
</head>
<body>
    <h1>Voting Eligibility Checker</h1>

    <form method="post">
        Name: <input type="text" name="name" required><br><br>
        Age: <input type="number" name="age" required><br><br>
        <input type="submit" value="Check Eligibility">
    </form>

    <%
    String name = request.getParameter("name");
    String ageStr = request.getParameter("age");

    if (name != null && ageStr != null) {
        int age = Integer.parseInt(ageStr);
        if (age >= 18) {
            out.println("<p>" + name + ", you are eligible to vote!</p>");
        } else {
            out.println("<p>" + name + ", you are not eligible to vote. Minimum age is 18.</p>");
        }
    }
    %>

</body>
</html>

B) Write a Java program to display given extension files from a specific directory on server machine.
Java Code (FileExtensionFilter.java):
import java.io.File;
import java.io.FilenameFilter;

public class FileExtensionFilter {

    public static void main(String[] args) {
        if (args.length != 2) {
            System.out.println("Usage: java FileExtensionFilter <directory_path> <file_extension>");
            System.out.println("Example: java FileExtensionFilter C:/my_documents txt");
            return;
        }

        String directoryPath = args[0];
        String fileExtension = args[1];

        File directory = new File(directoryPath);

        if (!directory.isDirectory()) {
            System.out.println("Error: '" + directoryPath + "' is not a valid directory.");
            return;
        }

        File[] files = directory.listFiles(new FilenameFilter() {
            @Override
            public boolean accept(File dir, String name) {
                return name.toLowerCase().endsWith("." + fileExtension.toLowerCase());
            }
        });

        if (files != null && files.length > 0) {
            System.out.println("Files with extension '." + fileExtension + "' in directory '" + directoryPath + "':");
            for (File file : files) {
                System.out.println(file.getName());
            }
        } else {
            System.out.println("No files with extension '." + fileExtension + "' found in directory '" + directoryPath + "'.");
        }
    }
}

A) Write a program in C#.Net to find the sum of all elements of the array.
C# Code (SumArray.cs):
using System;

public class SumArray
{
    public static void Main(string[] args)
    {
        int[] numbers = { 1, 2, 3, 4, 5 }; // Example array, you can modify this
        int sum = 0;

        // Calculate the sum of array elements
        for (int i = 0; i < numbers.Length; i++)
        {
            sum += numbers[i];
        }

        Console.WriteLine("Sum of array elements: " + sum);
    }
}

B) Write a C#.Net Program to define a class Person having members -name, address. Create a subclass called employee with member staffed, salary. Create ‘n’ objects of the Employee class and display all the details of the Employee.
C# Code (EmployeeDetails.cs):
using System;

// Define the Person class
public class Person
{
    public string Name { get; set; }
    public string Address { get; set; }

    public Person(string name, string address)
    {
        Name = name;
        Address = address;
    }

    public virtual void DisplayDetails()
    {
        Console.WriteLine("Name: " + Name);
        Console.WriteLine("Address: " + Address);
    }
}

// Define the Employee subclass inheriting from Person
public class Employee : Person
{
    public string StaffId { get; set; } // Assuming 'staffed' meant Staff ID
    public double Salary { get; set; }

    public Employee(string name, string address, string staffId, double salary) : base(name, address)
    {
        StaffId = staffId;
        Salary = salary;
    }

    public override void DisplayDetails()
    {
        base.DisplayDetails(); // Call Person's DisplayDetails to show name and address
        Console.WriteLine("Staff ID: " + StaffId);
        Console.WriteLine("Salary: $" + Salary);
        Console.WriteLine("--------------------");
    }
}

public class EmployeeDetails
{
    public static void Main(string[] args)
    {
        Console.Write("Enter the number of employees (n): ");
        int n = int.Parse(Console.ReadLine());

        Employee[] employees = new Employee[n];

        // Input employee details
        for (int i = 0; i < n; i++)
        {
            Console.WriteLine("\nEnter details for Employee " + (i + 1) + ":");
            Console.Write("Name: ");
            string name = Console.ReadLine();
            Console.Write("Address: ");
            string address = Console.ReadLine();
            Console.Write("Staff ID: ");
            string staffId = Console.ReadLine();
            Console.Write("Salary: ");
            double salary = double.Parse(Console.ReadLine());

            employees[i] = new Employee(name, address, staffId, salary);
        }

        Console.WriteLine("\nEmployee Details:");
        // Display employee details
        for (int i = 0; i < n; i++)
        {
            employees[i].DisplayDetails();
        }
    }
}
