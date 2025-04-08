Question A: Java program to display IP Address and name of client machine
Solution:
import java.net.InetAddress;
import java.net.UnknownHostException;

public class IPAddressName {
    public static void main(String[] args) {
        try {
            InetAddress localhost = InetAddress.getLocalHost();
            String hostName = localhost.getHostName();
            String ipAddress = localhost.getHostAddress();

            System.out.println("Client Machine Name: " + hostName);
            System.out.println("Client Machine IP Address: " + ipAddress);

        } catch (UnknownHostException e) {
            System.err.println("Error: Unable to determine client machine information.");
            e.printStackTrace();
        }
    }
}

Question B: Java program to display sales details between two selected dates
Solution:
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Scanner;

public class SalesDetails {

    // Database credentials (Replace with your actual credentials)
    static final String DB_URL = "jdbc:mysql://localhost:3306/your_database_name"; // Replace with your database URL
    static final String DB_USER = "your_db_user";       // Replace with your database username
    static final String DB_PASSWORD = "your_db_password";   // Replace with your database password

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter Start Date (YYYY-MM-DD): ");
        String startDate = scanner.nextLine();
        System.out.print("Enter End Date (YYYY-MM-DD): ");
        String endDate = scanner.nextLine();

        String sqlQuery = "SELECT PID, PName, Qty, Rate, Amount FROM Sales WHERE SaleDate BETWEEN '" + startDate + "' AND '" + endDate + "'";

        try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery(sqlQuery)) {

            System.out.println("\n--- Sales Details between " + startDate + " and " + endDate + " ---");
            System.out.printf("%-10s %-20s %-8s %-8s %-10s%n", "PID", "ProductName", "Quantity", "Rate", "Amount");
            System.out.println("------------------------------------------------------------");

            while (rs.next()) {
                int pid = rs.getInt("PID");
                String productName = rs.getString("PName");
                int quantity = rs.getInt("Qty");
                double rate = rs.getDouble("Rate");
                double amount = rs.getDouble("Amount");

                System.out.printf("%-10d %-20s %-8d %-8.2f %-10.2f%n", pid, productName, quantity, rate, amount);
            }

        } catch (SQLException e) {
            System.err.println("Database Error: " + e.getMessage());
            e.printStackTrace();
        } finally {
            scanner.close();
        }
    }
}


For C# (Default.aspx.cs):
using System;

public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        if (!IsPostBack)
        {
            PaymentModeDropdown.Items.Insert(0, new System.Web.UI.WebControls.ListItem("--Select--", ""));
        }
    }

    protected void ValidationButton_Click(object sender, EventArgs e)
    {
        if (Page.IsValid)
        {
            ValidationSummaryLabel.Text = "Validation Successful!";
            ValidationSummaryLabel.Visible = true;
            // Here you can process the validated data, e.g., save to database, etc.
            // For demonstration, let's just display the entered values.
            string userName = UserNameTextBox.Text;
            string paymentMode = PaymentModeDropdown.SelectedItem.Text;
            string creditCard = CreditCardTextBox.Text;

            ValidationSummaryLabel.Text += "<br/>User Name: " + userName;
            ValidationSummaryLabel.Text += "<br/>Payment Mode: " + paymentMode;
            ValidationSummaryLabel.Text += "<br/>Credit Card Number: " + creditCard;
        }
        else
        {
            ValidationSummaryLabel.Visible = false; // Hide success message if validation fails again
        }
    }
}
Use code with caution.
C#
For VB.NET (Default.aspx.vb):
Imports System

Partial Class _Default
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs) Handles Me.Load
        If Not IsPostBack Then
            PaymentModeDropdown.Items.Insert(0, New System.Web.UI.WebControls.ListItem("--Select--", ""))
        End If
    End Sub

    Protected Sub ValidationButton_Click(ByVal sender As Object, ByVal e As EventArgs) Handles ValidationButton.Click
        If Page.IsValid Then
            ValidationSummaryLabel.Text = "Validation Successful!"
            ValidationSummaryLabel.Visible = True
            ' Here you can process the validated data, e.g., save to database, etc.
            ' For demonstration, let's just display the entered values.
            Dim userName As String = UserNameTextBox.Text
            Dim paymentMode As String = PaymentModeDropdown.SelectedItem.Text
            Dim creditCard As String = CreditCardTextBox.Text

            ValidationSummaryLabel.Text &= "<br/>User Name: " & userName
            ValidationSummaryLabel.Text &= "<br/>Payment Mode: " & paymentMode
            ValidationSummaryLabel.Text &= "<br/>Credit Card Number: " & creditCard
        Else
            ValidationSummaryLabel.Visible = False ' Hide success message if validation fails again
        End If
    End Sub
End Class

Write the C# Code (Program.cs):
Open Program.cs.
Replace the existing code with the following:
using System;

class Fruit
{
    protected int count;

    public Fruit()
    {
        count = 0;
    }

    public virtual void SetCount(int num)
    {
        count = num;
    }

    public virtual int GetCount()
    {
        return count;
    }
}

class Apple : Fruit
{
    public Apple() : base() { } // Calls base class constructor

    public override void SetCount(int num)
    {
        base.SetCount(num); // Reuse base class logic, or customize if needed
    }

    public override int GetCount()
    {
        return base.GetCount();
    }
}

class Mango : Fruit
{
    public Mango() : base() { } // Calls base class constructor

    public override void SetCount(int num)
    {
        base.SetCount(num); // Reuse base class logic, or customize if needed
    }
    public override int GetCount()
    {
        return base.GetCount();
    }
}

class Program
{
    static void Main(string[] args)
    {
        Apple apples = new Apple();
        Mango mangoes = new Mango();

        apples.SetCount(5); // 5 apples in the basket
        mangoes.SetCount(3); // 3 mangoes in the basket

        int totalFruits = apples.GetCount() + mangoes.GetCount();

        Console.WriteLine("Number of apples in the basket: " + apples.GetCount());
        Console.WriteLine("Number of mangoes in the basket: " + mangoes.GetCount());
        Console.WriteLine("Total number of fruits in the basket: " + totalFruits);

        Console.ReadKey(); // To keep the console window open until a key is pressed
    }
}
Run the Application:
Press Ctrl + F5 (or click "Debug" -> "Start Without Debugging") to run the application.
A console window will open, displaying the output:
Number of apples in the basket: 5
Number of mangoes in the basket: 3
Total number of fruits in the basket: 8
