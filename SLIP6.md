Question A: Blinking Image on Frame (Java Swing)
Solution:
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class BlinkingImage extends JFrame {

    private ImageIcon imageIcon;
    private JLabel imageLabel;
    private boolean isVisible = true;
    private Timer timer;

    public BlinkingImage() {
        setTitle("Blinking Image");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(300, 300);
        setLayout(new FlowLayout());

        // Load your image (replace "your_image.png" with your image file path)
        imageIcon = new ImageIcon("your_image.png"); // Ensure image is in project root or provide full path
        imageLabel = new JLabel(imageIcon);
        add(imageLabel);

        // Timer to control blinking
        timer = new Timer(500, new ActionListener() { // Blink every 500 milliseconds
            @Override
            public void actionPerformed(ActionEvent e) {
                isVisible = !isVisible;
                imageLabel.setVisible(isVisible);
            }
        });
        timer.start(); // Start the timer to begin blinking

        setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(BlinkingImage::new);
    }
}


Question B: Servlet to Count User Visits (Servlet & Cookies)
Solution:
import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/visit") // Servlet URL mapping
public class VisitCounterServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        int visitCount = 0;
        Cookie[] cookies = request.getCookies();
        Cookie visitCookie = null;

        if (cookies != null) {
            for (Cookie cookie : cookies) {
                if (cookie.getName().equals("visitCount")) {
                    visitCookie = cookie;
                    visitCount = Integer.parseInt(cookie.getValue());
                    break;
                }
            }
        }

        visitCount++;

        if (visitCookie == null) {
            out.println("<h1>Welcome! This is your first visit.</h1>");
            visitCookie = new Cookie("visitCount", String.valueOf(visitCount));
        } else {
            out.println("<h1>You have visited this page " + visitCount + " times.</h1>");
            visitCookie.setValue(String.valueOf(visitCount));
        }

        response.addCookie(visitCookie); // Add or update the cookie in the response
    }
}
Deployment (using Tomcat as an example):
Create a folder structure for your web application, for instance, webapp.
Inside webapp, create a WEB-INF folder, and inside WEB-INF, create a classes folder.
Place the compiled VisitCounterServlet.class file into the webapp/WEB-INF/classes folder.
Create a web.xml file inside webapp/WEB-INF with the following content to configure your servlet (if you are not using annotations or if your servlet container needs explicit configuration):
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

  <servlet>
    <servlet-name>VisitCounterServlet</servlet-name>
    <servlet-class>VisitCounterServlet</servlet-class>
  </servlet>

  <servlet-mapping>
    <servlet-name>VisitCounterServlet</servlet-name>
    <url-pattern>/visit</url-pattern>
  </servlet-mapping>

</web-app>

3. Design the Flowers.aspx page (HTML and ASP.NET Controls):
Open Flowers.aspx in Design view (or Source view in VS 2010, or directly edit the .aspx file in VS Code). Add the following code within the <form> tags:
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Flowers.aspx.cs" Inherits="FlowerWebApp.Flowers" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Flower Selection</title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <h2>Select a Flower:</h2>
        <asp:RadioButtonList ID="RadioButtonListFlowers" runat="server" RepeatColumns="2">
        </asp:RadioButtonList>
        <br />
        <asp:Button ID="ButtonSubmit" runat="server" Text="Submit" OnClick="ButtonSubmit_Click" />
        <br />
        <br />
        <asp:Label ID="LabelSelectedFlower" runat="server" Text=""></asp:Label>
    </div>
    </form>
</body>
</html>
Use code with caution.
Html
4. Code-Behind (Flowers.aspx.cs or Flowers.aspx.vb):
Open the code-behind file (Flowers.aspx.cs for C# or Flowers.aspx.vb for VB.NET). Add the following code:
C# (Flowers.aspx.cs):
using System;
using System.Web.UI;

namespace FlowerWebApp
{
    public partial class Flowers : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            if (!IsPostBack) // Populate only on the first page load
            {
                RadioButtonListFlowers.Items.Add("Rose");
                RadioButtonListFlowers.Items.Add("Lily");
                RadioButtonListFlowers.Items.Add("Tulip");
                RadioButtonListFlowers.Items.Add("Sunflower");
                RadioButtonListFlowers.Items.Add("Orchid");
                RadioButtonListFlowers.Items.Add("Daisy");
            }
        }

        protected void ButtonSubmit_Click(object sender, EventArgs e)
        {
            if (RadioButtonListFlowers.SelectedItem != null)
            {
                LabelSelectedFlower.Text = "You selected: " + RadioButtonListFlowers.SelectedItem.Text;
            }
            else
            {
                LabelSelectedFlower.Text = "Please select a flower.";
            }
        }
    }
}
Use code with caution.
C#
VB.NET (Flowers.aspx.vb - if you chose VB.NET project):
Imports System

Partial Class Flowers
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs) Handles Me.Load
        If Not IsPostBack Then ' Populate only on the first page load
            RadioButtonListFlowers.Items.Add("Rose")
            RadioButtonListFlowers.Items.Add("Lily")
            RadioButtonListFlowers.Items.Add("Tulip")
            RadioButtonListFlowers.Items.Add("Sunflower")
            RadioButtonListFlowers.Items.Add("Orchid")
            RadioButtonListFlowers.Items.Add("Daisy")
        End If
    End Sub

    Protected Sub ButtonSubmit_Click(ByVal sender As Object, ByVal e As EventArgs) Handles ButtonSubmit.Click
        If RadioButtonListFlowers.SelectedItem IsNot Nothing Then
            LabelSelectedFlower.Text = "You selected: " & RadioButtonListFlowers.SelectedItem.Text
        Else
            LabelSelectedFlower.Text = "Please select a flower."
        End If
    End Sub
End Class

 Database Code in DatabaseModule.vb (using MS Access as example - requires Microsoft.ACE.OLEDB provider):
Imports System.Data.OleDb
Imports System.Windows.Forms ' For MessageBox

Module DatabaseModule

    Public Sub CreateMovieTable()
        Dim connectionString As String = "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=MovieDatabase.accdb;" ' Create Access database file in project directory
        Dim connection As OleDbConnection = New OleDbConnection(connectionString)
        Dim command As OleDbCommand = New OleDbCommand()

        Try
            connection.Open()
            command.Connection = connection
            command.CommandText = "CREATE TABLE Movies (Mv_Name VARCHAR(255), Release_year INT, Director VARCHAR(255))"
            command.ExecuteNonQuery()
            MessageBox.Show("Movie table created successfully.", "Success")
        Catch ex As OleDbException
            ' Check if table already exists (Error code -2147217887)
            If ex.ErrorCode = -2147217887 Then
                ' Table might already exist, ignore error in this simple example
                MessageBox.Show("Movie table might already exist.", "Information")
            Else
                MessageBox.Show("Error creating table: " & ex.Message, "Error")
            End If
        Catch ex As Exception
            MessageBox.Show("General error: " & ex.Message, "Error")
        Finally
            If connection.State = System.Data.ConnectionState.Open Then
                connection.Close()
            End If
        End Try
    End Sub

    Public Sub InsertMovieRecords()
        Dim connectionString As String = "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=MovieDatabase.accdb;"
        Dim connection As OleDbConnection = New OleDbConnection(connectionString)
        Dim command As OleDbCommand = New OleDbCommand()

        Try
            connection.Open()
            command.Connection = connection

            ' Insert up to 5 records (example data)
            Dim movies As String()() = {
                {"Movie A", "2020", "Director 1"},
                {"Movie B", "2021", "Director 2"},
                {"Movie C", "2022", "Director 3"},
                {"Movie D", "2023", "Director 4"},
                {"Movie E", "2022", "Director 5"}
            }

            For Each movie As String() In movies
                command.CommandText = "INSERT INTO Movies (Mv_Name, Release_year, Director) VALUES (@Name, @Year, @Director)"
                command.Parameters.Clear() ' Clear parameters before adding new ones
                command.Parameters.AddWithValue("@Name", movie(0))
                command.Parameters.AddWithValue("@Year", Integer.Parse(movie(1)))
                command.Parameters.AddWithValue("@Director", movie(2))
                command.ExecuteNonQuery()
            Next

            MessageBox.Show("Movie records inserted successfully.", "Success")

        Catch ex As OleDbException
            MessageBox.Show("Error inserting records: " & ex.Message, "Error")
        Catch ex As Exception
            MessageBox.Show("General error: " & ex.Message, "Error")
        Finally
            If connection.State = System.Data.ConnectionState.Open Then
                connection.Close()
            End If
        End Try
    End Sub

    Public Sub DeleteMoviesReleasedIn2022()
        Dim connectionString As String = "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=MovieDatabase.accdb;"
        Dim connection As OleDbConnection = New OleDbConnection(connectionString)
        Dim command As OleDbCommand = New OleDbCommand()

        Try
            connection.Open()
            command.Connection = connection
            command.CommandText = "DELETE FROM Movies WHERE Release_year = 2022"
            Dim rowsAffected As Integer = command.ExecuteNonQuery()

            MessageBox.Show(rowsAffected.ToString() & " movie(s) released in 2022 deleted.", "Deletion Result")

        Catch ex As OleDbException
            MessageBox.Show("Error deleting records: " & ex.Message, "Error")
        Catch ex As Exception
            MessageBox.Show("General error: " & ex.Message, "Error")
        Finally
            If connection.State = System.Data.ConnectionState.Open Then
                connection.Close()
            End If
        End Try
    End Sub

End Module
Use code with caution.
Vb.net
4. Call Database Functions from Form (e.g., Form1.vb):
Open Form1.vb (or the main form of your application). In the Form_Load event or a Button Click event (for example, add a Button to the form and double-click it to create a ButtonClick event handler), call the database functions:
Public Class Form1

    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
        ' Call database operations here or in a button click event
    End Sub

    Private Sub ButtonRunDatabaseOperations_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
        CreateMovieTable() ' Create table if not exists
        InsertMovieRecords() ' Insert movie records
        DeleteMoviesReleasedIn2022() ' Delete movies from 2022
    End Sub
End Class



