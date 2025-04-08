A)
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

class Student {
    String name;
    String rollNumber;
    String course;

    public Student(String name, String rollNumber, String course) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.course = course;
    }

    @Override
    public String toString() {
        return "Student{" +
               "name='" + name + '\'' +
               ", rollNumber='" + rollNumber + '\'' +
               ", course='" + course + '\'' +
               '}';
    }
}

public class DeleteStudents {
    public static void main(String[] args) {
        // Sample student data
        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice", "101", "Computer Science"));
        students.add(new Student("Bob", "102", "Mathematics"));
        students.add(new Student("Sophia", "103", "Physics"));
        students.add(new Student("Sam", "104", "Chemistry"));
        students.add(new Student("Charlie", "105", "Biology"));
        students.add(new Student("Sara", "106", "History"));

        System.out.println("Original Student List:");
        for (Student student : students) {
            System.out.println(student);
        }

        // Delete students whose name starts with 'S'
        Iterator<Student> iterator = students.iterator();
        while (iterator.hasNext()) {
            Student student = iterator.next();
            if (student.name.startsWith("S")) {
                iterator.remove(); // Use iterator to avoid ConcurrentModificationException
            }
        }

        System.out.println("\nStudent List after deleting students starting with 'S':");
        for (Student student : students) {
            System.out.println(student);
        }
    }
}

B)
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletContext;
import javax.servlet.ServletConfig;
import java.util.Enumeration;

@WebServlet(name = "InfoServlet", urlPatterns = {"/info"})
public class InfoServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        out.println("<html><head><title>Servlet Information</title></head><body>");
        out.println("<h1>Servlet Information</h1>");

        out.println("<h2>Client Request Information:</h2>");
        out.println("<p><strong>Client IP Address:</strong> " + request.getRemoteAddr() + "</p>");
        out.println("<p><strong>Browser Type (User-Agent):</strong> " + request.getHeader("User-Agent") + "</p>");

        out.println("<h2>Server Information:</h2>");
        out.println("<p><strong>Operating System:</strong> " + System.getProperty("os.name") + "</p>");

        out.println("<h2>Loaded Servlets:</h2>");
        ServletContext context = getServletContext();
        Enumeration<String> servletNames = context.getServletNames();
        out.println("<ul>");
        while (servletNames.hasMoreElements()) {
            out.println("<li>" + servletNames.nextElement() + "</li>");
        }
        out.println("</ul>");

        out.println("</body></html>");
    }
}
Question A: VB.net Form with DateTimePicker


Public Class Form1

    Private Sub dateTimePicker1_ValueChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles dateTimePicker1.ValueChanged
        txtDay.Text = dateTimePicker1.Value.Day.ToString()
        txtMonth.Text = dateTimePicker1.Value.Month.ToString()
        txtYear.Text = dateTimePicker1.Value.Year.ToString()
    End Sub
End Class


SQL Table Creation Script (in SQL Server Management Studio or similar tool):

CREATE TABLE Department (
    DeptId INT PRIMARY KEY,
    DeptName VARCHAR(50),
    EmpName VARCHAR(50),
    Salary DECIMAL(10, 2)
);

Imports System.Data.SqlClient

Partial Class _Default
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
        If Not IsPostBack Then
            PerformDatabaseOperations()
        End If
    End Sub

    Private Sub PerformDatabaseOperations()
        Dim connectionString As String = "Data Source=YourServerName;Initial Catalog=TestDB;Integrated Security=True" ' Replace with your SQL Server connection details

        Using connection As New SqlConnection(connectionString)
            Try
                connection.Open()

                ' 1. Insert 3 Records
                InsertRecords(connection)
                Response.Write("<p>Records Inserted.</p>")

                ' 2. Update Salary
                UpdateSalary(connection, "Employee2", 15) ' Update salary for EmpName 'Employee2' by 15%
                Response.Write("<p>Salary Updated.</p>")

                ' 3. Delete One Row
                DeleteRecord(connection, "Employee3") ' Delete row where EmpName is 'Employee3'
                Response.Write("<p>Record Deleted.</p>")


            Catch ex As Exception
                Response.Write("<p>Error: " & ex.Message & "</p>")
            Finally
                connection.Close()
            End Try
        End Using
    End Sub

    Private Sub InsertRecords(ByVal connection As SqlConnection)
        Dim insertSql As String = "INSERT INTO Department (DeptId, DeptName, EmpName, Salary) VALUES " &
                                  "(1, 'IT', 'Employee1', 50000), " &
                                  "(2, 'HR', 'Employee2', 60000), " &
                                  "(3, 'Finance', 'Employee3', 70000)"
        Using command As New SqlCommand(insertSql, connection)
            command.ExecuteNonQuery()
        End Using
    End Sub

    Private Sub UpdateSalary(ByVal connection As SqlConnection, ByVal empName As String, ByVal percentageIncrease As Decimal)
        Dim updateSql As String = "UPDATE Department SET Salary = Salary * (1 + @PercentageIncrease / 100) WHERE EmpName = @EmpName"
        Using command As New SqlCommand(updateSql, connection)
            command.Parameters.AddWithValue("@PercentageIncrease", percentageIncrease)
            command.Parameters.AddWithValue("@EmpName", empName)
            command.ExecuteNonQuery()
        End Using
    End Sub

    Private Sub DeleteRecord(ByVal connection As SqlConnection, ByVal empName As String)
        Dim deleteSql As String = "DELETE FROM Department WHERE EmpName = @EmpName"
        Using command As New SqlCommand(deleteSql, connection)
            command.Parameters.AddWithValue("@EmpName", empName)
            command.ExecuteNonQuery()
        End Using
    End Sub
End Class
