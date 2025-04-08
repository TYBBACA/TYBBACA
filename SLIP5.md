Q.1. A) JSP Program to Calculate Sum of First and Last Digit
JSP Code (sum_digits.jsp):
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>Sum of First and Last Digit</title>
</head>
<body>
<%
    int number = 12345; // You can change this number
    int lastDigit = number % 10;
    int firstNumber = number;
    while (firstNumber >= 10) {
        firstNumber = firstNumber / 10;
    }
    int sum = firstNumber + lastDigit;
%>

<p style="color:red; font-size:18px;">
    Sum of first and last digit of <%= number %> is: <%= sum %>
</p>

</body>
</html>


Q.1. B) Java Program for Traffic Signal using Applet and Multithreading
Java Code (TrafficSignalApplet.java):
import java.applet.Applet;
import java.awt.*;

public class TrafficSignalApplet extends Applet implements Runnable {
    Thread thread;
    Color redColor, yellowColor, greenColor;
    int signalState = 0; // 0: Red, 1: Yellow, 2: Green
    int x = 50, y = 50, diameter = 50;

    public void init() {
        redColor = Color.gray;
        yellowColor = Color.gray;
        greenColor = Color.gray;
        thread = new Thread(this);
        thread.start();
    }

    public void paint(Graphics g) {
        // Draw black background for signal box
        g.setColor(Color.BLACK);
        g.fillRect(x - 10, y - 10, diameter + 20, 3 * diameter + 30);

        // Draw Red light
        g.setColor(redColor);
        g.fillOval(x, y, diameter, diameter);
        g.setColor(Color.BLACK);
        g.drawOval(x, y, diameter, diameter);

        // Draw Yellow light
        g.setColor(yellowColor);
        g.fillOval(x, y + diameter + 10, diameter, diameter);
        g.setColor(Color.BLACK);
        g.drawOval(x, y + diameter + 10, diameter, diameter);

        // Draw Green light
        g.setColor(greenColor);
        g.fillOval(x, y + 2 * (diameter + 10), diameter, diameter);
        g.setColor(Color.BLACK);
        g.drawOval(x, y + 2 * (diameter + 10), diameter, diameter);
    }

    public void run() {
        while (true) {
            try {
                switch (signalState) {
                    case 0: // Red
                        redColor = Color.red;
                        yellowColor = Color.gray;
                        greenColor = Color.gray;
                        repaint();
                        Thread.sleep(5000); // Red for 5 seconds
                        signalState = 1;
                        break;
                    case 1: // Yellow
                        redColor = Color.gray;
                        yellowColor = Color.yellow;
                        greenColor = Color.gray;
                        repaint();
                        Thread.sleep(2000); // Yellow for 2 seconds
                        signalState = 2;
                        break;
                    case 2: // Green
                        redColor = Color.gray;
                        yellowColor = Color.gray;
                        greenColor = Color.green;
                        repaint();
                        Thread.sleep(5000); // Green for 5 seconds
                        signalState = 0;
                        break;
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public void stop() {
        if (thread != null) {
            thread.stop(); // deprecated but for simple applet example
            thread = null;
        }
    }
}
Create an HTML file:
Create a new text file named traffic.html (or any name with .html extension) in the same directory.
Add the following HTML code to traffic.html:
<!DOCTYPE html>
<html>
<head>
    <title>Traffic Signal Applet</title>
</head>
<body>
    <applet code="TrafficSignalApplet.class" width="200" height="300">
    </applet>
</body>
</html>




Q.2. A) VB.NET Program to Check Vowel/Consonant and Case
VB.NET Code (Module1.vb):
Module Module1

    Sub Main()
        Console.WriteLine("Enter a character: ")
        Dim inputChar As String = Console.ReadLine()

        If String.IsNullOrEmpty(inputChar) OrElse inputChar.Length > 1 Then
            Console.WriteLine("Invalid input. Please enter a single character.")
            Console.ReadKey()
            Return
        End If

        Dim ch As Char = Char.ToLower(inputChar(0)) ' Convert to lowercase for easier vowel check
        Dim caseType As String = ""
        Dim type As String = ""

        If Char.IsUpper(inputChar(0)) Then
            caseType = "Uppercase"
        ElseIf Char.IsLower(inputChar(0)) Then
            caseType = "Lowercase"
        Else
            caseType = "Not an alphabet case" 'Handle non-alphabetic characters if needed
        End If


        Select Case ch
            Case "a", "e", "i", "o", "u"
                type = "Vowel"
            Case Else
                type = "Consonant"
        End Select

        If type = "Vowel" OrElse type = "Consonant" Then
            Console.WriteLine($"The character '{inputChar}' is a {caseType} {type}.")
        Else
            Console.WriteLine($"The character '{inputChar}' is {caseType}.")
        End If


        Console.ReadKey() ' Pause to see the output
    End Sub

End Module



Q.2. B) ASP.NET Web Application for Simple Interest Calculation
ASP.NET Web Form Code (Default.aspx):
<%@ Page Language="vb" AutoEventWireup="false" CodeBehind="Default.aspx.vb" Inherits="WebApplication1._Default" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Simple Interest Calculator</title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <h2>Simple Interest Calculator</h2>
            <br />
            <asp:Label ID="lblLoanAmount" runat="server" Text="Loan Amount:"></asp:Label>
            <asp:TextBox ID="txtLoanAmount" runat="server"></asp:TextBox>
            <asp:RequiredFieldValidator ID="rfvLoanAmount" runat="server" ControlToValidate="txtLoanAmount" ErrorMessage="Loan Amount is required." ForeColor="Red"></asp:RequiredFieldValidator>
            <asp:RegularExpressionValidator ID="revLoanAmount" runat="server" ControlToValidate="txtLoanAmount" ErrorMessage="Loan Amount must be numeric." ForeColor="Red" ValidationExpression="^\d*\.?\d+$"></asp:RegularExpressionValidator>
            <br /><br />

            <asp:Label ID="lblInterestRate" runat="server" Text="Interest Rate (%):"></asp:Label>
            <asp:TextBox ID="txtInterestRate" runat="server"></asp:TextBox>
            <asp:RequiredFieldValidator ID="rfvInterestRate" runat="server" ControlToValidate="txtInterestRate" ErrorMessage="Interest Rate is required." ForeColor="Red"></asp:RequiredFieldValidator>
            <asp:RegularExpressionValidator ID="revInterestRate" runat="server" ControlToValidate="txtInterestRate" ErrorMessage="Interest Rate must be numeric." ForeColor="Red" ValidationExpression="^\d*\.?\d+$"></asp:RegularExpressionValidator>
            <br /><br />

            <asp:Label ID="lblDuration" runat="server" Text="Duration (Years):"></asp:Label>
            <asp:TextBox ID="txtDuration" runat="server"></asp:TextBox>
            <asp:RequiredFieldValidator ID="rfvDuration" runat="server" ControlToValidate="txtDuration" ErrorMessage="Duration is required." ForeColor="Red"></asp:RequiredFieldValidator>
            <asp:RegularExpressionValidator ID="revDuration" runat="server" ControlToValidate="txtDuration" ErrorMessage="Duration must be numeric." ForeColor="Red" ValidationExpression="^\d+$"></asp:RegularExpressionValidator>
            <br /><br />

            <asp:Button ID="btnCalculate" runat="server" Text="Calculate Interest" OnClick="btnCalculate_Click" />
            <br /><br />

            <asp:Label ID="lblSimpleInterestResult" runat="server" Text="Simple Interest: "></asp:Label>
            <asp:Label ID="lblSimpleInterestValue" runat="server" Text="" Font-Bold="true"></asp:Label>
            <br />
            <asp:ValidationSummary ID="ValidationSummary1" runat="server" HeaderText="Please correct the following errors:" ForeColor="Red" />

        </div>
    </form>
</body>
</html>
Use code with caution.
Html
ASP.NET Code-Behind (Default.aspx.vb):
Partial Class _Default
    Inherits System.Web.UI.Page

    Protected Sub btnCalculate_Click(sender As Object, e As EventArgs) Handles btnCalculate.Click
        If Page.IsValid Then ' Check if all validators are valid
            Dim loanAmount As Double
            Dim interestRate As Double
            Dim duration As Integer

            If Double.TryParse(txtLoanAmount.Text, loanAmount) AndAlso Double.TryParse(txtInterestRate.Text, interestRate) AndAlso Integer.TryParse(txtDuration.Text, duration) Then

                Dim simpleInterest As Double = (loanAmount * interestRate * duration) / 100

                lblSimpleInterestValue.Text = simpleInterest.ToString("C") ' "C" for currency format

            Else
                ' This case should ideally not be reached if validators are set up correctly, but for extra safety
                lblSimpleInterestValue.Text = "Invalid Input"
            End If
        End If
    End Sub
End Class


