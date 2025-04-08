Question A: Write a Java program to display each alphabet after 2 seconds between 'a' to 'z'.
Java Code:
public class AlphabetDisplay {

    public static void main(String[] args) {
        for (char alphabet = 'a'; alphabet <= 'z'; alphabet++) {
            System.out.println(alphabet);
            try {
                Thread.sleep(2000); // 2000 milliseconds = 2 seconds
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}


Question B: Write a Java program to accept the details of Student (RNo, SName, Per, Gender, Class) and store them into the database. (Use appropriate Swing Components and PreparedStatement Interface).
This is a more complex question involving Swing GUI and database interaction. For simplicity and to demonstrate the core concepts, I will provide a basic Swing application that takes input and then shows how to use PreparedStatement to insert data. Note: You will need to set up a database (like MySQL) and have the JDBC driver for your database in your classpath to run this successfully.
Java Code:
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class StudentDatabaseApp extends JFrame implements ActionListener {

    private JLabel rollNoLabel, nameLabel, percentageLabel, genderLabel, classLabel;
    private JTextField rollNoField, nameField, percentageField, classField;
    private JComboBox<String> genderComboBox;
    private JButton submitButton;

    public StudentDatabaseApp() {
        setTitle("Student Details Form");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(6, 2)); // Grid layout for labels and fields

        rollNoLabel = new JLabel("Roll No:");
        rollNoField = new JTextField();
        nameLabel = new JLabel("Name:");
        nameField = new JTextField();
        percentageLabel = new JLabel("Percentage:");
        percentageField = new JTextField();
        genderLabel = new JLabel("Gender:");
        genderComboBox = new JComboBox<>(new String[]{"Male", "Female", "Other"});
        classLabel = new JLabel("Class:");
        classField = new JTextField();
        submitButton = new JButton("Submit");

        submitButton.addActionListener(this);

        add(rollNoLabel);
        add(rollNoField);
        add(nameLabel);
        add(nameField);
        add(percentageLabel);
        add(percentageField);
        add(genderLabel);
        add(genderComboBox);
        add(classLabel);
        add(classField);
        add(new JLabel()); // Empty label for spacing
        add(submitButton);

        pack(); // Adjusts frame size to fit components
        setLocationRelativeTo(null); // Center the frame
        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == submitButton) {
            try {
                int rollNo = Integer.parseInt(rollNoField.getText());
                String name = nameField.getText();
                double percentage = Double.parseDouble(percentageField.getText());
                String gender = (String) genderComboBox.getSelectedItem();
                String className = classField.getText();

                // Database connection details (Replace with your actual details)
                String url = "jdbc:mysql://localhost:3306/your_database_name"; // Replace with your database URL
                String username = "your_username";       // Replace with your database username
                String password = "your_password";       // Replace with your database password

                Connection connection = DriverManager.getConnection(url, username, password);

                String sql = "INSERT INTO students (roll_no, student_name, percentage, gender, class) VALUES (?, ?, ?, ?, ?)";
                PreparedStatement preparedStatement = connection.prepareStatement(sql);
                preparedStatement.setInt(1, rollNo);
                preparedStatement.setString(2, name);
                preparedStatement.setDouble(3, percentage);
                preparedStatement.setString(4, gender);
                preparedStatement.setString(5, className);

                int rowsInserted = preparedStatement.executeUpdate();
                if (rowsInserted > 0) {
                    JOptionPane.showMessageDialog(this, "Data inserted successfully!");
                } else {
                    JOptionPane.showMessageDialog(this, "Failed to insert data.");
                }

                preparedStatement.close();
                connection.close();

            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(this, "Invalid input. Please check Roll No and Percentage.");
            } catch (SQLException ex) {
                JOptionPane.showMessageDialog(this, "Database error: " + ex.getMessage());
                ex.printStackTrace(); // For debugging purposes, print the full exception
            }
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new StudentDatabaseApp());
    }
}

Question 2.A) ASP.NET Application
Solution Steps:
Create an ASP.NET Web Forms Application:
Open Visual Studio Code (or your .NET development environment).
You'll need to ensure you have the .NET Framework SDK installed and the C# extension for VS Code.
Create a new project. If you're using VS Code, you might need to use the .NET CLI or a project template generator to create an ASP.NET Web Forms project (as VS Code doesn't directly provide the full project creation GUI for .NET Framework as Visual Studio IDE does). You can use the command line:
dotnet new webforms -o ColorWebApp
cd ColorWebApp
Use code with caution.
Bash
(This assumes you have the .NET SDK installed and configured to target .NET Framework. You might need to adjust if targeting a specific framework version.)
Create a User Control (ColorListControl.ascx):
Inside your project, create a new file named ColorListControl.ascx (in VS Code, you can right-click in the Explorer pane and create a new file).
Add the following code to ColorListControl.ascx:
<%@ Control Language="C#" AutoEventWireup="true" CodeBehind="ColorListControl.ascx.cs" Inherits="ColorWebApp.ColorListControl" %>

<asp:DropDownList ID="ddlColors" runat="server">
    <asp:ListItem Value="White">White</asp:ListItem>
    <asp:ListItem Value="Red">Red</asp:ListItem>
    <asp:ListItem Value="Green">Green</asp:ListItem>
    <asp:ListItem Value="Blue">Blue</asp:ListItem>
    <asp:ListItem Value="Yellow">Yellow</asp:ListItem>
</asp:DropDownList>
Use code with caution.
Aspx
Create the code-behind file ColorListControl.ascx.cs (if it's not automatically created, ensure the CodeBehind and Inherits attributes in .ascx are correct and create a C# file with the same name in the same directory). It will be initially empty, but it's good practice to have it.
Create or Modify the Web Form (Default.aspx):
Open your default Web Form (e.g., Default.aspx or WebForm1.aspx, depending on your project template).
Add the User Control and a Button to the form. Modify the Default.aspx to look like this:
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="ColorWebApp.Default" %>

<%@ Register TagPrefix="uc" TagName="ColorList" Src="ColorListControl.ascx" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Color Changer</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <uc:ColorList ID="ColorListControl1" runat="server" />
            <asp:Button ID="btnChangeColor" runat="server" Text="Change Color" OnClick="btnChangeColor_Click" />
        </div>
    </form>
</body>
</html>
Use code with caution.
Aspx
Code-Behind for Web Form (Default.aspx.cs):
Open the code-behind file for your Web Form (e.g., Default.aspx.cs).
Add the following C# code to handle the button click event:
using System;

namespace ColorWebApp
{
    public partial class Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void btnChangeColor_Click(object sender, EventArgs e)
        {
            string selectedColor = ColorListControl1.ddlColors.SelectedValue;
            form1.Style["background-color"] = selectedColor;
        }
    }
}


Question 2.B) C#.NET Program
Solution Steps:
Create a C# Console Application:
In VS Code (or your .NET environment), create a new project. If using .NET CLI:
dotnet new console -o CustomerDetailsApp
cd CustomerDetailsApp
Use code with caution.
Bash
Write the C# Code (Program.cs):
Open the Program.cs file in your project.
Replace the existing code with the following C# code:
using System;
using System.Collections.Generic;

namespace CustomerDetailsApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Enter the number of customers (n):");
            int n = int.Parse(Console.ReadLine());

            List<Customer> customers = new List<Customer>();
            double totalAllItemsPrice = 0;

            for (int i = 0; i < n; i++)
            {
                Console.WriteLine($"\nEnter details for Customer {i + 1}:");

                Console.Write("Customer No: ");
                int customerNo = int.Parse(Console.ReadLine());

                Console.Write("Name: ");
                string name = Console.ReadLine();

                Console.Write("Address: ");
                string address = Console.ReadLine();

                Console.Write("Item No: ");
                string itemNo = Console.ReadLine();

                Console.Write("Quantity: ");
                int quantity = int.Parse(Console.ReadLine());

                Console.Write("Price per item: ");
                double price = double.Parse(Console.ReadLine());

                Customer customer = new Customer(customerNo, name, address, itemNo, quantity, price);
                customers.Add(customer);
            }

            Console.WriteLine("\n--- Customer Details ---");
            foreach (var customer in customers)
            {
                customer.DisplayDetails();
                totalAllItemsPrice += customer.TotalPrice;
            }

            Console.WriteLine("\n--- Summary ---");
            Console.WriteLine($"Total price of all items from all customers: ${totalAllItemsPrice}");

            Console.ReadKey(); // Keep console window open until a key is pressed
        }
    }

    class Customer
    {
        public int CustomerNo { get; set; }
        public string Name { get; set; }
        public string Address { get; set; }
        public string ItemNo { get; set; }
        public int Quantity { get; set; }
        public double Price { get; set; }
        public double TotalPrice { get; private set; }

        public Customer(int customerNo, string name, string address, string itemNo, int quantity, double price)
        {
            CustomerNo = customerNo;
            Name = name;
            Address = address;
            ItemNo = itemNo;
            Quantity = quantity;
            Price = price;
            TotalPrice = Quantity * Price;
        }

        public void DisplayDetails()
        {
            Console.WriteLine($"\nCustomer No: {CustomerNo}");
            Console.WriteLine($"Name: {Name}");
            Console.WriteLine($"Address: {Address}");
            Console.WriteLine($"Item No: {ItemNo}");
            Console.WriteLine($"Quantity: {Quantity}");
            Console.WriteLine($"Price per item: ${Price}");
            Console.WriteLine($"Total Price for this item: ${TotalPrice}");
        }
    }
}

