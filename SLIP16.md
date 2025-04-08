Create index.html (Login Form):
This HTML file will contain the form for users to enter their username and password.
<!DOCTYPE html>
<html>
<head>
    <title>Login Form</title>
</head>
<body>
    <h2>Login</h2>
    <form action="login.jsp" method="post">
        Username: <input type="text" name="username"><br><br>
        Password: <input type="password" name="password"><br><br>
        <input type="submit" value="Login">
    </form>
</body>
</html>
Use code with caution.
Html
Create login.jsp (JSP Script for Login Processing):
This JSP file will receive the username and password from the form, compare them, and redirect accordingly.
<%@ page import="java.util.Objects" %>
<%
    String enteredUsername = request.getParameter("username");
    String enteredPassword = request.getParameter("password");

    // **Hardcoded Correct Credentials (For demonstration purposes)**
    String correctUsername = "user123";
    String correctPassword = "password123";

    if (Objects.equals(enteredUsername, correctUsername) && Objects.equals(enteredPassword, correctPassword)) {
        response.sendRedirect("Login.html"); // Redirect to Login.html for success
    } else {
        response.sendRedirect("Error.html"); // Redirect to Error.html for failure
    }
%>
Use code with caution.
Jsp
Create Login.html (Login Success Page):
This HTML file will be displayed upon successful login.
<!DOCTYPE html>
<html>
<head>
    <title>Login Successful</title>
</head>
<body>
    <h2>Login Successful!</h2>
    <p>Welcome!</p>
</body>
</html>
Use code with caution.
Html
Create Error.html (Login Failure Page):
This HTML file will be displayed upon login failure.
<!DOCTYPE html>
<html>
<head>
    <title>Login Failed</title>
</head>
<body>
    <h2>Login Failed!</h2>
    <p>Invalid username or password.</p>
</body>
</html>

B) Java Program for Student Data (using PreparedStatement):
Database Setup (Example using MySQL):
Install MySQL: If you don't have MySQL, install it.
Create Database and Table:
Connect to your MySQL server (using MySQL command line client or a tool like MySQL Workbench) and execute the following SQL commands:
CREATE DATABASE student_db;
USE student_db;
CREATE TABLE students (
    rno INT PRIMARY KEY,
    sname VARCHAR(255),
    per DECIMAL(5, 2)
);
Use code with caution.
SQL
Java Program (StudentData.java):
import java.sql.*;
import java.util.Scanner;

public class StudentData {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        ResultSet resultSet = null;

        try {
            // Database connection details (Modify as per your MySQL setup)
            String url = "jdbc:mysql://localhost:3306/student_db"; // Replace with your database URL
            String username = "your_mysql_username";        // Replace with your MySQL username
            String password = "your_mysql_password";        // Replace with your MySQL password

            // Load JDBC driver for MySQL (Make sure you have MySQL Connector/J in your classpath)
            Class.forName("com.mysql.cj.jdbc.Driver"); // For newer MySQL Connector/J versions
            connection = DriverManager.getConnection(url, username, password);

            // Accept student details for at least 5 records
            for (int i = 0; i < 5; i++) {
                System.out.println("Enter details for student " + (i + 1) + ":");
                System.out.print("Roll Number: ");
                int rno = scanner.nextInt();
                scanner.nextLine(); // Consume newline
                System.out.print("Student Name: ");
                String sname = scanner.nextLine();
                System.out.print("Percentage: ");
                double per = scanner.nextDouble();
                scanner.nextLine(); // Consume newline

                // Prepare SQL INSERT statement using PreparedStatement
                String insertSQL = "INSERT INTO students (rno, sname, per) VALUES (?, ?, ?)";
                preparedStatement = connection.prepareStatement(insertSQL);
                preparedStatement.setInt(1, rno);
                preparedStatement.setString(2, sname);
                preparedStatement.setDouble(3, per);

                int rowsInserted = preparedStatement.executeUpdate();
                if (rowsInserted > 0) {
                    System.out.println("Student record inserted successfully.");
                } else {
                    System.out.println("Failed to insert student record.");
                }
                preparedStatement.close(); // Close PreparedStatement after each use
            }

            // Find student with highest percentage
            String selectMaxPercentageSQL = "SELECT * FROM students ORDER BY per DESC LIMIT 1";
            preparedStatement = connection.prepareStatement(selectMaxPercentageSQL);
            resultSet = preparedStatement.executeQuery();

            if (resultSet.next()) {
                System.out.println("\nStudent with the highest percentage:");
                System.out.println("Roll Number: " + resultSet.getInt("rno"));
                System.out.println("Name: " + resultSet.getString("sname"));
                System.out.println("Percentage: " + resultSet.getDouble("per"));
            } else {
                System.out.println("No student records found.");
            }

        } catch (ClassNotFoundException e) {
            System.err.println("JDBC Driver not found: " + e.getMessage());
        } catch (SQLException e) {
            System.err.println("Database error: " + e.getMessage());
        } finally {
            // Close resources in finally block
            try {
                if (resultSet != null) resultSet.close();
                if (preparedStatement != null) preparedStatement.close();
                if (connection != null) connection.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
            scanner.close();
        }
    }
}


A) ASP.NET User Control for Login Validation:


Design User Control (LoginControl.ascx):
Open LoginControl.ascx in Design view or Source view and add the following markup:
<%@ Control Language="C#" AutoEventWireup="true" CodeBehind="LoginControl.ascx.cs" Inherits="WebAppLogin.LoginControl" %>

<div>
    <h2>Login</h2>
    Username: <asp:TextBox ID="txtUsername" runat="server"></asp:TextBox><br /><br />
    Password: <asp:TextBox ID="txtPassword" runat="server" TextMode="Password"></asp:TextBox><br /><br />
    <asp:Button ID="btnLogin" runat="server" Text="Login" OnClick="btnLogin_Click" /><br /><br />
    <asp:Label ID="lblStatus" runat="server" Text=""></asp:Label>
</div>
Use code with caution.
Html
Code-Behind for User Control (LoginControl.ascx.cs):
Open LoginControl.ascx.cs (or LoginControl.ascx.vb for VB) and add the following code:
using System;

namespace WebAppLogin
{
    public partial class LoginControl : System.Web.UI.UserControl
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void btnLogin_Click(object sender, EventArgs e)
        {
            string username = txtUsername.Text;
            string password = txtPassword.Text;

            if (username == "DYP" && password == "Pimpri")
            {
                lblStatus.Text = "User Authorized";
            }
            else
            {
                lblStatus.Text = "User Not Authorized";
            }
        }
    }
}
Use code with caution.
C#
Add Web Form to Host User Control:
In Solution Explorer, right-click on your project name (WebAppLogin).
Go to Add -> New Item....
Select "Web Form". Name it LoginPage.aspx and click "Add".
Use User Control in Web Form (LoginPage.aspx):
Open LoginPage.aspx in Design view or Source view. In the <form> tag, register and use your User Control:
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="LoginPage.aspx.cs" Inherits="WebAppLogin.LoginPage" %>

<%@ Register Src="LoginControl.ascx" TagName="LoginControl" TagPrefix="uc1" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Login Page</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <h1>ASP.NET Login Validation</h1>
            <uc1:LoginControl ID="LoginControl1" runat="server" />
        </div>
    </form>
</body>
</html>

B) C# .Net Program for Supplier Class and Input/Output:

Define Supplier Class (Program.cs):
Open Program.cs and add the Supplier class definition inside the namespace:
using System;

namespace SupplierApp
{
    class Supplier
    {
        public int sid { get; set; }
        public string name { get; set; }
        public string address { get; set; }
        public string pincode { get; set; }

        public override string ToString() // Override ToString for easy display
        {
            return $"Supplier ID: {sid}, Name: {name}, Address: {address}, Pincode: {pincode}";
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Enter the number of suppliers:");
            int n = int.Parse(Console.ReadLine());

            Supplier[] suppliers = new Supplier[n]; // Array to store suppliers

            for (int i = 0; i < n; i++)
            {
                Supplier supplier = new Supplier();
                Console.WriteLine($"\nEnter details for supplier {i + 1}:");

                Console.Write("Supplier ID: ");
                supplier.sid = int.Parse(Console.ReadLine());

                Console.Write("Name: ");
                supplier.name = Console.ReadLine();

                Console.Write("Address: ");
                supplier.address = Console.ReadLine();

                Console.Write("Pincode: ");
                supplier.pincode = Console.ReadLine();

                suppliers[i] = supplier; // Store supplier in array
            }

            Console.WriteLine("\nSupplier Details:");
            foreach (Supplier sup in suppliers)
            {
                Console.WriteLine(sup); // Use overridden ToString method
            }

            Console.ReadKey(); // Keep console window open until key press
        }
    }
}
