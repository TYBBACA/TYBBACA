Question 1A: JDBC Program to Delete Employee Details
Solution:
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class DeleteEmployee {

    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("Usage: java DeleteEmployee <employee_id>");
            return;
        }

        int employeeId = Integer.parseInt(args[0]);
        String jdbcUrl = "jdbc:mysql://localhost:3306/your_database_name"; // Replace with your database URL
        String username = "your_username"; // Replace with your database username
        String password = "your_password"; // Replace with your database password

        try {
            // 1. Load the JDBC driver (MySQL in this case) - optional for newer JDBC versions
            Class.forName("com.mysql.cj.jdbc.Driver"); // Or your specific driver

            // 2. Establish connection
            Connection connection = DriverManager.getConnection(jdbcUrl, username, password);

            // 3. Prepare SQL DELETE statement
            String deleteSql = "DELETE FROM employees WHERE ENO = ?"; // Assuming table name is 'employees'
            PreparedStatement preparedStatement = connection.prepareStatement(deleteSql);
            preparedStatement.setInt(1, employeeId);

            // 4. Execute the DELETE statement
            int rowsAffected = preparedStatement.executeUpdate();

            // 5. Check if deletion was successful
            if (rowsAffected > 0) {
                System.out.println("Employee with ID " + employeeId + " deleted successfully.");
            } else {
                System.out.println("Employee with ID " + employeeId + " not found.");
            }

            // 6. Close resources
            preparedStatement.close();
            connection.close();

        } catch (ClassNotFoundException e) {
            System.err.println("JDBC Driver not found: " + e.getMessage());
        } catch (SQLException e) {
            System.err.println("Database error: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.err.println("Invalid Employee ID. Please enter a number.");
        }
    }
}


Question 1B: Java Multithreading Applet for Drawing Temple
Solution:
import java.applet.Applet;
import java.awt.Graphics;
import java.awt.Color;

public class TempleApplet extends Applet implements Runnable {

    private int flagX = 50; // Initial X position of the flag
    private Thread animationThread;

    @Override
    public void init() {
        setBackground(Color.WHITE);
    }

    @Override
    public void start() {
        if (animationThread == null) {
            animationThread = new Thread(this);
            animationThread.start();
        }
    }

    @Override
    public void stop() {
        if (animationThread != null) {
            animationThread = null; // Allow thread to stop
        }
    }

    @Override
    public void run() {
        while (Thread.currentThread() == animationThread) {
            try {
                repaint(); // Request repaint to trigger paint method
                Thread.sleep(50); // Delay for animation speed (milliseconds)
                flagX = (flagX + 2) % 200; // Simple animation: move flag horizontally
                if (flagX > 190) flagX = 50; // Reset flag position
            } catch (InterruptedException e) {
                break; // Exit thread if interrupted
            }
        }
    }

    @Override
    public void paint(Graphics g) {
        // Draw Temple Structure
        g.setColor(Color.GRAY);
        g.fillRect(50, 150, 100, 100); // Base of temple
        g.fillRect(70, 100, 60, 50);   // Middle part
        g.fillRect(80, 50, 40, 50);    // Top part
        g.setColor(Color.RED);
        g.fillPolygon(new int[]{80, 120, 100}, new int[]{50, 50, 20}, 3); // Temple peak

        // Draw Flag (animated)
        g.setColor(Color.BLUE);
        g.fillRect(flagX, 40, 20, 10); // Flag pole
        g.setColor(Color.YELLOW);
        g.fillRect(flagX, 30, 20, 10); // Flag itself (yellow for visibility)
    }
}

Create an HTML file to run the Applet:
Create a text file named temple.html (or any name with .html extension) in the same directory as TempleApplet.class.
Paste the following HTML code into temple.html:
<!DOCTYPE html>
<html>
<head>
    <title>Temple Applet</title>
</head>
<body>
    <applet code="TempleApplet.class" width="300" height="300">
    </applet>
</body>
</html>




Question 2A: VB.NET Program for Sample Tree View Control
Solution (VB.NET Code):
Public Class Form1
    Inherits System.Windows.Forms.Form

#Region " Windows Form Designer generated code "

    Public Sub New()
        MyBase.New

        'This call is required by the Windows Form Designer.
        InitializeComponent()

        'Add any initialization after the InitializeComponent() call

    End Sub

    'Form overrides dispose to clean up the component list.
    Protected Overloads Overrides Sub Dispose(ByVal disposing As Boolean)
        If disposing Then
            If Not (components Is Nothing) Then
                components.Dispose()
            End If
        End If
        MyBase.Dispose(disposing)
    End Sub

    'Required by the Windows Form Designer
    Private components As System.ComponentModel.IContainer

    'NOTE: The following procedure is required by the Windows Form Designer
    'It can be modified using the Windows Form Designer.
    'Do not modify it using the code editor.
    Friend WithEvents TreeView1 As System.Windows.Forms.TreeView

    <System.Diagnostics.DebuggerStepThrough()> Private Sub InitializeComponent()
        Me.TreeView1 = New System.Windows.Forms.TreeView()
        Me.SuspendLayout()
        '
        'TreeView1
        '
        Me.TreeView1.Location = New System.Drawing.Point(16, 16)
        Me.TreeView1.Name = "TreeView1"
        Me.TreeView1.Size = New System.Drawing.Size(264, 240)
        Me.TreeView1.TabIndex = 0
        '
        'Form1
        '
        Me.AutoScaleBaseSize = New System.Drawing.Size(5, 13)
        Me.ClientSize = New System.Drawing.Size(292, 273)
        Me.Controls.Add(Me.TreeView1)
        Me.Name = "Form1"
        Me.Text = "Sample TreeView"
        Me.ResumeLayout(False)

    End Sub

#End Region

    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
        ' Add root node
        Dim rootNode As TreeNode = New TreeNode("Root Node")
        TreeView1.Nodes.Add(rootNode)

        ' Add child nodes to the root node
        Dim childNode1 As TreeNode = New TreeNode("Child Node 1")
        rootNode.Nodes.Add(childNode1)

        Dim childNode2 As TreeNode = New TreeNode("Child Node 2")
        rootNode.Nodes.Add(childNode2)

        ' Add grandchild nodes to Child Node 2
        Dim grandchildNode1 As TreeNode = New TreeNode("Grandchild Node 1")
        childNode2.Nodes.Add(grandchildNode1)

        Dim grandchildNode2 As TreeNode = New TreeNode("Grandchild Node 2")
        childNode2.Nodes.Add(grandchildNode2)

        ' Expand the root node to show children
        rootNode.Expand()
    End Sub
End Class

Question 2B: ASP.NET Web Application for Exception Handling
Solution (ASP.NET Code and Configuration):
1. Default.aspx (Web Form):
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Default.aspx.vb" Inherits="_Default" Trace="true" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Exception Handling Demo</title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <asp:Button ID="Button1" runat="server" Text="Generate Exception" OnClick="Button1_Click" />
    </div>
    </form>
</body>
</html>
Use code with caution.
Aspx
2. Default.aspx.vb (Code-Behind):
Partial Class _Default
    Inherits System.Web.UI.Page

    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs) Handles Button1.Click
        Try
            Dim numbers As Integer() = {1, 2, 3}
            Dim value As Integer = numbers(5) ' This will cause IndexOutOfRangeException
        Catch ex As IndexOutOfRangeException
            ' Redirect to custom error page
            Response.Redirect("CustomError.aspx")
        End Try
    End Sub
End Class
Use code with caution.
Vb.net
3. CustomError.aspx (Custom Error Page):
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="CustomError.aspx.vb" Inherits="CustomError" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Custom Error Page</title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <h1>Oops! An Error Occurred</h1>
        <p>Sorry, something went wrong. Please try again later.</p>
    </div>
    </form>
</body>
</html>
Use code with caution.
Aspx
4. Web.config (Configuration File - Add Custom Error Section):
<?xml version="1.0"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0"/>

    <customErrors mode="On" defaultRedirect="CustomError.aspx">
      <error statusCode="404" redirect="PageNotFound.aspx"/> <! -- Optional: Example for 404 errors -->
    </customErrors>

  </system.web>
</configuration>
