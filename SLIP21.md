Question A: Java program to display name and priority of a Thread
Solution:
// ThreadInfo.java
public class ThreadInfo extends Thread {

    @Override
    public void run() {
        Thread currentThread = Thread.currentThread();
        System.out.println("Thread Name: " + currentThread.getName());
        System.out.println("Thread Priority: " + currentThread.getPriority());
    }

    public static void main(String[] args) {
        ThreadInfo thread = new ThreadInfo();
        thread.setName("MyThread"); // Setting a custom name (optional)
        thread.start();
    }
}

Question B: Servlet program to accept student details, calculate percentage and grade
Solution:
// StudentServlet.java
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/StudentServlet")
public class StudentServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String seatNo = request.getParameter("seatNo");
        String studName = request.getParameter("studName");
        String className = request.getParameter("class");
        String totalMarksStr = request.getParameter("totalMarks");

        int totalMarks = 0;
        double percentage = 0.0;
        String grade = "Fail"; // Default grade

        try {
            totalMarks = Integer.parseInt(totalMarksStr);
            percentage = (double) totalMarks; // Assuming total marks is out of 100. Modify if needed.

            if (percentage >= 90) {
                grade = "A+";
            } else if (percentage >= 80) {
                grade = "A";
            } else if (percentage >= 70) {
                grade = "B";
            } else if (percentage >= 60) {
                grade = "C";
            } else if (percentage >= 50) {
                grade = "D";
            }
        } catch (NumberFormatException e) {
            grade = "Invalid Marks";
        }

        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        out.println("<!DOCTYPE html>");
        out.println("<html><head><title>Student Details</title></head><body>");
        out.println("<h1>Student Details</h1>");
        out.println("<p><strong>Seat No:</strong> " + seatNo + "</p>");
        out.println("<p><strong>Student Name:</strong> " + studName + "</p>");
        out.println("<p><strong>Class:</strong> " + className + "</p>");
        out.println("<p><strong>Total Marks:</strong> " + totalMarks + "</p>");
        out.println("<p><strong>Percentage:</strong> " + String.format("%.2f", percentage) + "%</p>"); // Format to 2 decimal places
        out.println("<p><strong>Grade:</strong> " + grade + "</p>");
        out.println("</body></html>");
    }
}
Use code with caution.
Java
HTML Form (to submit data to Servlet):
Create an HTML file (e.g., student_form.html) in the same directory as your web application's context root (or accessible from it):
<!DOCTYPE html>
<html>
<head>
    <title>Student Form</title>
</head>
<body>
    <h1>Enter Student Details</h1>
    <form action="StudentServlet" method="post">
        Seat No: <input type="text" name="seatNo"><br><br>
        Student Name: <input type="text" name="studName"><br><br>
        Class: <input type="text" name="class"><br><br>
        Total Marks (out of 100): <input type="text" name="totalMarks"><br><br>
        <input type="submit" value="Submit">
    </form>
</body>
</html>


Create web.xml (Deployment Descriptor - optional for simple servlets with annotations):
If you are not using @WebServlet annotation or need more configuration, create web.xml inside studentWebApp/WEB-INF/:
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                          http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>StudentServlet</servlet-name>
        <servlet-class>StudentServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>StudentServlet</servlet-name>
        <url-pattern>/StudentServlet</url-pattern>
    </servlet-mapping>
</web-app>

Question 2A: VB.NET program to count words in a textbox

Public Class Form1

    Private Sub ButtonCount_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles ButtonCount.Click
        Dim inputText As String = TextBoxInput.Text
        Dim words As String() = inputText.Split({" "c, vbCrLf}, StringSplitOptions.RemoveEmptyEntries) ' Split by space and newline
        Dim wordCount As Integer = words.Length

        MessageBox.Show("Number of words: " & wordCount, "Word Count")
    End Sub
End Class

Question 2B: ASP.NET application for EMP table operations


Design the Web Form (Employee.aspx):
Switch to "Design" view of Employee.aspx.
Drag and drop controls from the "Toolbox" to create input fields and buttons. You can use TextBox, Button, and Label controls.
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Employee.aspx.cs" Inherits="EmpWebApp.Employee" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Employee Management</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <h1>Employee Details</h1>
            <asp:Label ID="lblMessage" runat="server" Text="" ForeColor="Red"></asp:Label><br />

            Employee No: <asp:TextBox ID="txtEmpNo" runat="server"></asp:TextBox><br /><br />
            Employee Name: <asp:TextBox ID="txtEmpName" runat="server"></asp:TextBox><br /><br />
            Designation: <asp:TextBox ID="txtDesignation" runat="server"></asp:TextBox><br /><br />
            Salary: <asp:TextBox ID="txtSalary" runat="server"></asp:TextBox><br /><br />
            Joining Date (YYYY-MM-DD): <asp:TextBox ID="txtJoinDate" runat="server"></asp:TextBox><br /><br />

            <asp:Button ID="btnCreateTable" runat="server" Text="Create Table" OnClick="btnCreateTable_Click" /><br /><br />
            <asp:Button ID="btnInsert" runat="server" Text="Insert Record" OnClick="btnInsert_Click" /><br /><br />
            <asp:Button ID="btnUpdate" runat="server" Text="Update Record" OnClick="btnUpdate_Click" /><br />
        </div>
    </form>
</body>
</html>
Use code with caution.
Html
Write C# Code (Employee.aspx.cs):
Open the code-behind file Employee.aspx.cs.
Add necessary namespaces and code for database operations (using SQL Server Express as example, ensure you have it installed).
using System;
using System.Configuration;
using System.Data.SqlClient;

namespace EmpWebApp
{
    public partial class Employee : System.Web.UI.Page
    {
        string connectionString = "Data Source=.\\SQLEXPRESS;Initial Catalog=YourDatabaseName;Integrated Security=True"; // Replace YourDatabaseName

        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void btnCreateTable_Click(object sender, EventArgs e)
        {
            using (SqlConnection con = new SqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    string createTableQuery = "CREATE TABLE EMP (eno INT PRIMARY KEY, ename VARCHAR(50), edesignation VARCHAR(50), salary DECIMAL(10, 2), joindate DATE)";
                    SqlCommand cmd = new SqlCommand(createTableQuery, con);
                    cmd.ExecuteNonQuery();
                    lblMessage.Text = "Table EMP created successfully.";
                }
                catch (Exception ex)
                {
                    lblMessage.Text = "Error creating table: " + ex.Message;
                }
            }
        }

        protected void btnInsert_Click(object sender, EventArgs e)
        {
            using (SqlConnection con = new SqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    string insertQuery = "INSERT INTO EMP (eno, ename, edesignation, salary, joindate) VALUES (@eno, @ename, @edesignation, @salary, @joindate)";
                    SqlCommand cmd = new SqlCommand(insertQuery, con);
                    cmd.Parameters.AddWithValue("@eno", txtEmpNo.Text);
                    cmd.Parameters.AddWithValue("@ename", txtEmpName.Text);
                    cmd.Parameters.AddWithValue("@edesignation", txtDesignation.Text);
                    cmd.Parameters.AddWithValue("@salary", txtSalary.Text);
                    cmd.Parameters.AddWithValue("@joindate", txtJoinDate.Text);
                    int rowsAffected = cmd.ExecuteNonQuery();
                    if (rowsAffected > 0)
                    {
                        lblMessage.Text = "Record inserted successfully.";
                    }
                    else
                    {
                        lblMessage.Text = "Record insertion failed.";
                    }
                }
                catch (Exception ex)
                {
                    lblMessage.Text = "Error inserting record: " + ex.Message;
                }
            }
        }

        protected void btnUpdate_Click(object sender, EventArgs e)
        {
            using (SqlConnection con = new SqlConnection(connectionString))
            {
                try
                {
                    con.Open();
                    string updateQuery = "UPDATE EMP SET ename = @ename, edesignation = @edesignation, salary = @salary, joindate = @joindate WHERE eno = @eno";
                    SqlCommand cmd = new SqlCommand(updateQuery, con);
                    cmd.Parameters.AddWithValue("@eno", txtEmpNo.Text);
                    cmd.Parameters.AddWithValue("@ename", txtEmpName.Text);
                    cmd.Parameters.AddWithValue("@edesignation", txtDesignation.Text);
                    cmd.Parameters.AddWithValue("@salary", txtSalary.Text);
                    cmd.Parameters.AddWithValue("@joindate", txtJoinDate.Text);
                    int rowsAffected = cmd.ExecuteNonQuery();
                    if (rowsAffected > 0)
                    {
                        lblMessage.Text = "Record updated successfully.";
                    }
                    else
                    {
                        lblMessage.Text = "Record update failed. Employee No might not exist.";
                    }
                }
                catch (Exception ex)
                {
                    lblMessage.Text = "Error updating record: " + ex.Message;
                }
            }
        }
    }
}
