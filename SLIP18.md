Q.1. A) Write a java program to calculate factorial of a number. (Use sleep () method).
Java Program (FactorialSleep.java):
import java.util.Scanner;

public class FactorialSleep {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a non-negative integer: ");
        int number = scanner.nextInt();

        if (number < 0) {
            System.out.println("Factorial is not defined for negative numbers.");
            return;
        }

        long factorial = 1;
        System.out.println("Calculating factorial of " + number + "...");

        for (int i = 1; i <= number; i++) {
            factorial *= i;
            System.out.println("Step " + i + ": Current Factorial = " + factorial);
            try {
                Thread.sleep(500); // Pause for 0.5 seconds to demonstrate sleep()
            } catch (InterruptedException e) {
                System.out.println("Thread sleep interrupted!");
            }
        }

        System.out.println("\nFactorial of " + number + " = " + factorial);
        scanner.close();
    }
}

Q.1. B) Write a java program for simple standalone chatting application.
Java Program (SimpleChat.java):
import java.util.Scanner;

public class SimpleChat {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Simple Chat Application Started!");
        System.out.println("Type 'bye' to exit.");

        while (true) {
            System.out.print("You: ");
            String message = scanner.nextLine();

            if (message.equalsIgnoreCase("bye")) {
                System.out.println("ChatBot: Goodbye!");
                break; // Exit the loop and end chat
            }

            System.out.println("ChatBot: You said: " + message); // Simple echo as chatbot response
        }
        scanner.close();
        System.out.println("Chat Application Ended.");
    }
}


Q.2. A) VB.NET Program to display multiplication table in ListBox.
VB.NET Code (Form1.vb):
Public Class Form1

    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
        Dim number As Integer
        If Integer.TryParse(InputBox("Enter a number to see its multiplication table:", "Multiplication Table Input"), number) Then
            ListBox1.Items.Clear() ' Clear previous items
            For i As Integer = 1 To 10 ' Generate multiplication table up to 10
                ListBox1.Items.Add(number.ToString() & " x " & i.ToString() & " = " & (number * i).ToString())
            Next
        Else
            MessageBox.Show("Invalid input. Please enter a valid number.", "Input Error")
        End If
    End Sub
End Class


Q.2. B) ASP.NET Program for a store item display.
ASP.NET Code (Default.aspx):
<%@ Page Language="VB" AutoEventWireup="false" CodeFile="Default.aspx.vb" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Store Items</title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <h2>Store Items</h2>
        <asp:ListBox ID="ItemList" runat="server" AutoPostBack="True" OnSelectedIndexChanged="ItemList_SelectedIndexChanged"></asp:ListBox>
        <br />
        <asp:Image ID="ItemImage" runat="server" Width="150px" Height="150px" BorderStyle="Solid" BorderWidth="1px" />
        <br />
        <asp:Button ID="ShowCostButton" runat="server" Text="Show Cost" OnClick="ShowCostButton_Click" />
        <br />
        <asp:Label ID="CostLabel" runat="server" Text="Cost: "></asp:Label>
    </div>
    </form>
</body>
</html>
Use code with caution.
Html
ASP.NET Code (Default.aspx.vb):
Partial Class _Default
    Inherits System.Web.UI.Page

    ' Sample data - In real app, this would come from a database or config
    Private itemData As New System.Collections.Generic.Dictionary(Of String, ItemDetails)()

    Protected Sub Page_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Me.Load
        If Not IsPostBack Then ' Load data only on initial page load
            ' Sample Item Details (ItemName, ImageURL, Cost)
            itemData.Add("Item1", New ItemDetails("Item1", "images/item1.jpg", 25.0))
            itemData.Add("Item2", New ItemDetails("Item2", "images/item2.jpg", 50.0))
            itemData.Add("Item3", New ItemDetails("Item3", "images/item3.jpg", 75.0))

            ItemList.Items.Clear()
            For Each itemName As String In itemData.Keys
                ItemList.Items.Add(New System.Web.UI.WebControls.ListItem(itemData(itemName).Name, itemName))
            Next
        End If
    End Sub

    Protected Sub ItemList_SelectedIndexChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles ItemList.SelectedIndexChanged
        Dim selectedItemKey As String = ItemList.SelectedItem.Value
        If itemData.ContainsKey(selectedItemKey) Then
            ItemImage.ImageUrl = itemData(selectedItemKey).ImageURL
        Else
            ItemImage.ImageUrl = "" ' Clear image if item not found
        End If
    End Sub

    Protected Sub ShowCostButton_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles ShowCostButton.Click
        If Not String.IsNullOrEmpty(ItemList.SelectedItem.Value) Then
            Dim selectedItemKey As String = ItemList.SelectedItem.Value
            If itemData.ContainsKey(selectedItemKey) Then
                CostLabel.Text = "Cost: $" & itemData(selectedItemKey).Cost.ToString()
            Else
                CostLabel.Text = "Cost: Item details not found."
            End If
        Else
            CostLabel.Text = "Cost: Please select an item."
        End If
    End Sub

    ' Helper class to hold item details
    Private Class ItemDetails
        Public Property Name As String
        Public Property ImageURL As String
        Public Property Cost As Double

        Public Sub New(ByVal name As String, ByVal imageURL As String, ByVal cost As Double)
            Me.Name = name
            Me.ImageURL = imageURL
            Me.Cost = cost
        End Sub
    End Class
End Class
