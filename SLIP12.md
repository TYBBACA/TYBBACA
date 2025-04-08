Question A: Write a Java program to count the number of records in a table.
Solution:
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class CountRecords {

    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/your_database_name"; // Replace with your database URL
        String username = "your_username";       // Replace with your database username
        String password = "your_password";       // Replace with your database password
        String tableName = "your_table_name";    // Replace with your table name

        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        try {
            // 1. Load the JDBC driver (for MySQL, you might not need to explicitly load in newer versions)
            Class.forName("com.mysql.cj.jdbc.Driver"); // Or "com.mysql.jdbc.Driver" for older versions

            // 2. Establish connection
            connection = DriverManager.getConnection(url, username, password);

            // 3. Create statement
            statement = connection.createStatement();

            // 4. Execute SQL query to count records
            String sqlQuery = "SELECT COUNT(*) FROM " + tableName;
            resultSet = statement.executeQuery(sqlQuery);

            // 5. Retrieve the count
            resultSet.next();
            int count = resultSet.getInt(1);

            // 6. Print the count
            System.out.println("Number of records in table '" + tableName + "': " + count);

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // 7. Close resources in reverse order of creation
            try { if (resultSet != null) resultSet.close(); } catch (Exception e) { e.printStackTrace(); }
            try { if (statement != null) statement.close(); } catch (Exception e) { e.printStackTrace(); }
            try { if (connection != null) connection.close(); } catch (Exception e) { e.printStackTrace(); }
        }
    }
}
Use code with caution.

Question B: Write a program in Java which will show lifecycle (creation, sleep, and dead) of a thread. Program should print randomly the name of thread and value of sleep time. The name of the thread should be hard coded through constructor. The sleep time of a thread will be a random integer in the range 0 to 4999.
Solution:
import java.util.Random;

class MyThread extends Thread {
    private String threadName;

    public MyThread(String name) {
        this.threadName = name;
    }

    @Override
    public void run() {
        Random random = new Random();
        int sleepTime = random.nextInt(5000); // Generates random integer from 0 to 4999

        System.out.println("Thread '" + threadName + "' created.");

        System.out.println("Thread '" + threadName + "' will sleep for: " + sleepTime + " milliseconds.");
        try {
            Thread.sleep(sleepTime); // Thread goes to sleep
        } catch (InterruptedException e) {
            System.out.println("Thread '" + threadName + "' interrupted during sleep.");
            return; // End thread execution if interrupted
        }

        System.out.println("Thread '" + threadName + "' woke up and finished execution (dead).");
    }
}

public class ThreadLifecycle {
    public static void main(String[] args) {
        MyThread thread1 = new MyThread("FirstThread");
        MyThread thread2 = new MyThread("SecondThread");

        thread1.start(); // Start thread 1
        thread2.start(); // Start thread 2

        System.out.println("Main thread continues execution...");
    }
}



Code in ButtonColorChange.aspx:
Open ButtonColorChange.aspx in Design view or Source view.
Go to Source View (if you are in Design view, click on the "Source" tab at the bottom).
Replace the existing code with the following:
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="ButtonColorChange.aspx.vb" Inherits="ButtonColorChange" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Button Color Change</title>
    <style type="text/css">
        .greenButton {
            background-color: green;
            color: white; /* Optional: text color for better visibility */
            padding: 10px 20px;
            border: none;
            cursor: pointer;
        }

        .greenButton:hover {
            background-color: yellow;
            color: black; /* Optional: text color on hover */
        }
    </style>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Button ID="ColorButton" runat="server" Text="Hover Me!" CssClass="greenButton" />
        </div>
    </form>
</body>
</html>

Short and Clear Solution for 2.A:
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="ButtonColorChange.aspx.vb" Inherits="ButtonColorChange" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Button Color Change</title>
    <style type="text/css">
        .greenButton { background-color: green; color: white; padding: 10px 20px; border: none; cursor: pointer; }
        .greenButton:hover { background-color: yellow; color: black; }
    </style>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Button ID="ColorButton" runat="server" Text="Hover Me!" CssClass="greenButton" />
        </div>
    </form>
</body>
</html>

Code in Form1.vb:
Double-click on the loadDataButton to open the code editor for the button's Click event.
Replace the existing code in Form1.vb with the following:
Imports System.Data.SqlClient

Public Class Form1

    Private Sub loadDataButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles loadDataButton.Click
        Dim connectionString As String = "Data Source=.\\SQLEXPRESS;Initial Catalog=TestDB;Integrated Security=True;" ' Replace with your connection string
        Dim sqlConnection As SqlConnection = New SqlConnection(connectionString)

        Try
            sqlConnection.Open()

            ' 1. Create Table (if it doesn't exist)
            Dim createTableQuery As String = "IF NOT EXISTS (SELECT * FROM sysobjects WHERE name='player' and xtype='U') " & _
                                             "CREATE TABLE player (PID INT PRIMARY KEY, PName VARCHAR(255), Game VARCHAR(255), no_of_matches INT)"
            Dim createTableCommand As SqlCommand = New SqlCommand(createTableQuery, sqlConnection)
            createTableCommand.ExecuteNonQuery()

            ' 2. Insert Records (if table is empty - for demonstration, you might want to check if records exist before inserting in real scenario)
            Dim countRecordsQuery As String = "SELECT COUNT(*) FROM player"
            Dim countRecordsCommand As SqlCommand = New SqlCommand(countRecordsQuery, sqlConnection)
            Dim recordCount As Integer = Convert.ToInt32(countRecordsCommand.ExecuteScalar())

            If recordCount = 0 Then
                Dim insertQuery As String = "INSERT INTO player (PID, PName, Game, no_of_matches) VALUES " & _
                                             "(1, 'Virat Kohli', 'Cricket', 250), " & _
                                             "(2, 'Rohit Sharma', 'Cricket', 200), " & _
                                             "(3, 'Lionel Messi', 'Football', 300)"
                Dim insertCommand As SqlCommand = New SqlCommand(insertQuery, sqlConnection)
                insertCommand.ExecuteNonQuery()
            End If


            ' 3. Update 'Rohit Sharma' matches
            Dim updateQuery As String = "UPDATE player SET no_of_matches = 220 WHERE PName = 'Rohit Sharma'"
            Dim updateCommand As SqlCommand = New SqlCommand(updateQuery, sqlConnection)
            Dim rowsAffected As Integer = updateCommand.ExecuteNonQuery()
            Console.WriteLine(rowsAffected & " row(s) updated.") ' Optional: for debugging

            ' 4. Display Data in DataGridView
            Dim selectQuery As String = "SELECT * FROM player"
            Dim dataAdapter As SqlDataAdapter = New SqlDataAdapter(selectQuery, sqlConnection)
            Dim dataTable As DataTable = New DataTable()
            dataAdapter.Fill(dataTable)
            playerDataGridView.DataSource = dataTable

        Catch ex As Exception
            MessageBox.Show("Error: " & ex.Message)
        Finally
            If sqlConnection.State = ConnectionState.Open Then
                sqlConnection.Close()
            End If
        End Try
    End Sub
End Class


Short and Clear Solution for 2.B:
Imports System.Data.SqlClient

Public Class Form1
    Private Sub loadDataButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles loadDataButton.Click
        Dim connectionString As String = "Data Source=.\\SQLEXPRESS;Initial Catalog=TestDB;Integrated Security=True;" ' Your connection string
        Using sqlConnection As New SqlConnection(connectionString)
            Try
                sqlConnection.Open()
                ' Create Table (if not exists)
                Using createTableCommand As New SqlCommand("IF NOT EXISTS (SELECT * FROM sysobjects WHERE name='player' and xtype='U') CREATE TABLE player (PID INT PRIMARY KEY, PName VARCHAR(255), Game VARCHAR(255), no_of_matches INT)", sqlConnection)
                    createTableCommand.ExecuteNonQuery()
                End Using
                ' Insert Records (if empty)
                If Convert.ToInt32(New SqlCommand("SELECT COUNT(*) FROM player", sqlConnection).ExecuteScalar()) = 0 Then
                    Using insertCommand As New SqlCommand("INSERT INTO player (PID, PName, Game, no_of_matches) VALUES (1, 'Virat Kohli', 'Cricket', 250), (2, 'Rohit Sharma', 'Cricket', 200), (3, 'Lionel Messi', 'Football', 300)", sqlConnection)
                        insertCommand.ExecuteNonQuery()
                    End Using
                End If
                ' Update Rohit Sharma's matches
                Using updateCommand As New SqlCommand("UPDATE player SET no_of_matches = 220 WHERE PName = 'Rohit Sharma'", sqlConnection)
                    updateCommand.ExecuteNonQuery()
                End Using
                ' Display data
                Using dataAdapter As New SqlDataAdapter("SELECT * FROM player", sqlConnection)
                    Dim dataTable As New DataTable()
                    dataAdapter.Fill(dataTable)
                    playerDataGridView.DataSource = dataTable
                End Using
            Catch ex As Exception
                MessageBox.Show("Error: " & ex.Message)
            End Try
        End Using
    End Sub
End Class
