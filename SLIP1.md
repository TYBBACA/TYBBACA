SLIP 1
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleScrollingText extends JFrame implements ActionListener {

    private JLabel textLabel;
    private String text = "  Scrolling Text Example  "; 
    private int xPosition = 10; 
    private Timer timer;
    private boolean scrollRight = true;

    public SimpleScrollingText() {
        setTitle("Simple Scrolling Text");
        setSize(400, 100);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new FlowLayout(FlowLayout.LEFT)); 

        textLabel = new JLabel(text);
        textLabel.setFont(new Font("Arial", Font.BOLD, 16));
        add(textLabel);

        timer = new Timer(50, this); 
        timer.start();

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (scrollRight) {
            xPosition += 2; 
            if (xPosition > getWidth()) { 
                scrollRight = false; 
                xPosition = getWidth() - 2; 
            }
        } else {
            xPosition -= 2; 
            if (xPosition < -textLabel.getPreferredSize().width) {
                scrollRight = true; 
                xPosition = 10; 
            }
        }
        textLabel.setLocation(xPosition, 20); 
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new SimpleScrollingText());
    }
}

2nd
import javax.swing.*;
import java.awt.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class SimpleChatServer {

    private static List<PrintWriter> clientWriters = new ArrayList<>();
    private static JTextArea messageArea;

    public static void main(String[] args) throws IOException {
        JFrame frame = new JFrame("Simple Chat Server");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 300);

        messageArea = new JTextArea();
        messageArea.setEditable(false);
        JScrollPane scrollPane = new JScrollPane(messageArea);
        frame.add(scrollPane, BorderLayout.CENTER);
        frame.setVisible(true);

        try (ServerSocket serverSocket = new ServerSocket(5000)) {
            messageArea.append("Server started on port 5000...\n");
            while (true) {
                Socket clientSocket = serverSocket.accept();
                messageArea.append("Client connected: " + clientSocket.getInetAddress() + "\n");
                Thread clientThread = new Thread(() -> handleClient(clientSocket)); 
                clientThread.start();
            }
        } catch (IOException e) {
            messageArea.append("Server error: " + e.getMessage() + "\n");
            e.printStackTrace();
        }
    }

    private static void handleClient(Socket clientSocket) {
        PrintWriter writer = null;
        try {
            Scanner reader = new Scanner(clientSocket.getInputStream());
            writer = new PrintWriter(clientSocket.getOutputStream(), true);
            clientWriters.add(writer); 

            while (reader.hasNextLine()) {
                String message = reader.nextLine();
                messageArea.append("Received: " + message + "\n");
                broadcastMessage(message); 
            }
        } catch (IOException e) {
            messageArea.append("Client handler error: " + e.getMessage() + "\n");
            e.printStackTrace();
        } finally {
            if (writer != null) {
                clientWriters.remove(writer); 
            }
            try {
                clientSocket.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            messageArea.append("Client disconnected: " + clientSocket.getInetAddress() + "\n");
        }
    }

    private static void broadcastMessage(String message) {
        for (PrintWriter clientWriter : clientWriters) {
            clientWriter.println(message);
        }
    }
}
b
import javax.swing.*;
import java.awt.*;
import java.io.IOException;
import java.io.PrintWriter;
import java.net.Socket;
import java.util.Scanner;

public class SimpleChatClient {

    private static JTextArea messageArea;
    private static JTextField inputField;
    private static PrintWriter writer;

    public static void main(String[] args) {
        JFrame frame = new JFrame("Simple Chat Client");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 300);
        frame.setLayout(new BorderLayout());

        messageArea = new JTextArea();
        messageArea.setEditable(false);
        JScrollPane scrollPane = new JScrollPane(messageArea);
        frame.add(scrollPane, BorderLayout.CENTER);

        JPanel inputPanel = new JPanel(new BorderLayout());
        inputField = new JTextField();
        inputField.addActionListener(e -> sendMessage()); 
        JButton sendButton = new JButton("Send");
        sendButton.addActionListener(e -> sendMessage());
        inputPanel.add(inputField, BorderLayout.CENTER);
        inputPanel.add(sendButton, BorderLayout.EAST);
        frame.add(inputPanel, BorderLayout.SOUTH);

        frame.setVisible(true);

        try {
            Socket socket = new Socket("localhost", 5000);
            writer = new PrintWriter(socket.getOutputStream(), true);
            Scanner reader = new Scanner(socket.getInputStream());

            Thread readThread = new Thread(() -> { 
                while (reader.hasNextLine()) {
                    messageArea.append("Server: " + reader.nextLine() + "\n");
                }
            });
            readThread.start();

        } catch (IOException e) {
            messageArea.append("Could not connect to server.\n");
        }
    }

    private static void sendMessage() {
        String message = inputField.getText();
        if (!message.trim().isEmpty()) {
            writer.println(message); 
            inputField.setText("");   
        }
    }
}

vb
Public Class Form1
    Private numberCounter As Integer = 1
    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
        TextBox1.Text += numberCounter.ToString() + " "
        numberCounter += 1
    End Sub

    Private Sub TextBox1_TextChanged(sender As Object, e As EventArgs) Handles TextBox1.TextChanged

    End Sub
End Class

SLIP 1 A


2vb
Imports System.Data.SqlClient

Public Class Form1

    Private Sub btnSave_Click(sender As Object, e As EventArgs) Handles btnSave.Click
        Dim eno As Integer
        Dim ename As String
        Dim salary As Decimal

        If Not Integer.TryParse(txtENO.Text, eno) Then
            MessageBox.Show("Please enter a valid Employee Number (ENO).", "Input Error")
            Return
        End If

        ename = txtEName.Text

        If Not Decimal.TryParse(txtSalary.Text, salary) Then
            MessageBox.Show("Please enter a valid Salary.", "Input Error")
            Return
        End If

        Dim connectionString As String = "Data Source=(LocalDB)\MSSQLLocalDB;Integrated Security=True;AttachDbFilename=|DataDirectory|\EmployeeDB.mdf;Initial Catalog=EmployeeDB;"

        Using connection As New SqlConnection(connectionString)
            Try
                connection.Open()

                Dim createDbCommand As New SqlCommand("IF NOT EXISTS (SELECT name FROM master.databases WHERE name = 'EmployeeDB') CREATE DATABASE EmployeeDB;", connection)
                createDbCommand.ExecuteNonQuery()
                connection.ChangeDatabase("EmployeeDB")

                Dim createTableCommand As New SqlCommand("IF NOT EXISTS (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'Employee') CREATE TABLE Employee (ENO INT PRIMARY KEY, EName VARCHAR(255), Salary DECIMAL(10, 2));", connection)
                createTableCommand.ExecuteNonQuery()

                Dim insertQuery As String = "INSERT INTO Employee (ENO, EName, Salary) VALUES (@ENO, @EName, @Salary)"
                Using command As New SqlCommand(insertQuery, connection)
                    command.Parameters.AddWithValue("@ENO", eno)
                    command.Parameters.AddWithValue("@EName", ename)
                    command.Parameters.AddWithValue("@Salary", salary)
                    command.ExecuteNonQuery()
                    MessageBox.Show("Employee data saved successfully!", "Success")
                    LoadEmployeeData()
                    txtENO.Clear()
                    txtEName.Clear()
                    txtSalary.Clear()
                End Using

            Catch ex As Exception
                MessageBox.Show("Error saving data: " & ex.Message, "Database Error")
            Finally
                connection.Close()
            End Try
        End Using
    End Sub

    Private Sub LoadEmployeeData()
        Dim connectionString As String = "Data Source=(LocalDB)\MSSQLLocalDB;Integrated Security=True;AttachDbFilename=|DataDirectory|\EmployeeDB.mdf;Initial Catalog=EmployeeDB;"

        Using connection As New SqlConnection(connectionString)
            Try
                connection.Open()
                Dim query As String = "SELECT ENO, EName, Salary FROM Employee"
                Using adapter As New SqlDataAdapter(query, connection)
                    Dim employeeDataTable As New DataTable()
                    adapter.Fill(employeeDataTable)
                    dgvEmployee.DataSource = employeeDataTable
                End Using
            Catch ex As Exception
                MessageBox.Show("Error loading employee data: " & ex.Message, "Database Error")
            Finally
                connection.Close()
            End Try
        End Using
    End Sub

    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        LoadEmployeeData()
    End Sub
End Class

Create LoadEmployeeData Subroutine to Display in GridView: Add this subroutine within your Form1 class (but outside any event handlers):
Private Sub LoadEmployeeData()
    Dim connectionString As String = "Data Source=(LocalDB)\MSSQLLocalDB;Integrated Security=True;AttachDbFilename=|DataDirectory|\EmployeeDB.mdf;Initial Catalog=EmployeeDB;"

    Using connection As New SqlConnection(connectionString)
        Try
            connection.Open()
            Dim query As String = "SELECT ENO, EName, Salary FROM Employee"
            Using adapter As New SqlDataAdapter(query, connection)
                Dim employeeDataTable As New DataTable()
                adapter.Fill(employeeDataTable)
                dgvEmployee.DataSource = employeeDataTable ' Bind DataTable to GridView
            End Using
        Catch ex As Exception
            MessageBox.Show("Error loading employee data: " & ex.Message, "Database Error")
        Finally
            connection.Close()
        End Try
    End Using
End Sub

SLIP 1 END 

SLIP 2
