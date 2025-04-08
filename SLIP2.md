JAVA
A)
 perfectNumberLogic.jsp (Logic file to be included):
<%!
    public boolean isPerfectNumber(int num) {
        if (num <= 1) return false;
        int sum = 1;
        for (int i = 2; i * i <= num; i++) {
            if (num % i == 0) {
                sum += i;
                if (i * i != num) {
                    sum += num / i;
                }
            }
        }
        return sum == num;
    }
%>
<%
    String numStr = request.getParameter("number");
    boolean isPerfect = false;
    String message = "";
    if (numStr != null && !numStr.isEmpty()) {
        try {
            int number = Integer.parseInt(numStr);
            isPerfect = isPerfectNumber(number);
            if (isPerfect) {
                message = number + " is a perfect number.";
            } else {
                message = number + " is not a perfect number.";
            }
        } catch (NumberFormatException e) {
            message = "Invalid number format.";
        }
    } else {
        message = "Please enter a number.";
    }
%>
Use code with caution.
Jsp
2. perfectNumberChecker.jsp (Main JSP file):
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>Perfect Number Checker</title>
</head>
<body>
    <h1>Perfect Number Checker</h1>
    <form method="get">
        Enter a number: <input type="text" name="number">
        <input type="submit" value="Check">
    </form>
    <br>
    <%@ include file="perfectNumberLogic.jsp" %>
    <p><%= message %></p>
</body>
</html>


B)
FlagApplet.java (Java Applet Code):
import java.applet.Applet;
import java.awt.Graphics;
import java.awt.Color;

public class FlagApplet extends Applet implements Runnable {
    Thread flagThread;

    public void init() {
        flagThread = new Thread(this);
        flagThread.start();
    }

    public void run() {
        // For simple static flag, no continuous animation needed,
        // so thread can exit after first paint.
        repaint();
    }

    public void paint(Graphics g) {
        // Example: Drawing a simple tricolor flag (e.g., Indian Flag)
        int width = 200;
        int height = 120;
        int startX = 50;
        int startY = 50;

        // Saffron (Top band)
        g.setColor(Color.ORANGE);
        g.fillRect(startX, startY, width, height / 3);

        // White (Middle band)
        g.setColor(Color.WHITE);
        g.fillRect(startX, startY + height / 3, width, height / 3);

        // Green (Bottom band)
        g.setColor(Color.GREEN);
        g.fillRect(startX, startY + 2 * height / 3, width, height / 3);

        // Ashok Chakra (Simple blue circle in the white band)
        g.setColor(Color.BLUE);
        g.fillOval(startX + width / 2 - 15, startY + height / 3 + height / 6 - 15, 30, 30);
    }
}
Use code with caution.
Java
2. FlagApplet.html (HTML file to run the applet):
<!DOCTYPE html>
<html>
<head>
    <title>Flag Applet</title>
</head>
<body>
    <applet code="FlagApplet.class" width="300" height="200">
    </applet>
</body>
</html>


.NET
Q.2 Dot Net Framework:

A) VB.Net Program to Move Text "Pune University" (Left to Right and Vice Versa):

Steps to Run on Visual Studio 2010:

Open Visual Studio 2010: Launch Visual Studio 2010.

Create New Project:

Go to File -> New -> Project....

In the New Project dialog:

Under Installed Templates, select Visual Basic.

Choose Windows Forms Application.

Give a Name (e.g., MovingTextVB) and Location for your project.

Click OK.

Design the Form:

In the Form1.vb [Design] view:

Drag and drop a Label control from the Toolbox onto the form.

Set its Text property to "Pune University".

Set its AutoSize property to True.

Name it lblText (optional, but good practice).

Drag and drop a Timer control from the Toolbox onto the form. It will appear in the component tray below the form.

Name it tmrMoveText (optional).

Set its Interval property to 50 (adjust for speed, lower value for faster movement).

Set its Enabled property to True.

Write the Code:

Double-click on the Timer control on the form (or right-click and select View Code). This will open the Form1.vb code editor and create the tmrMoveText_Tick event handler.

Paste the following VB.Net code into Form1.vb:

Public Class Form1
    Dim direction As Integer = 1 ' 1 for right, -1 for left

    Private Sub tmrMoveText_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles tmrMoveText.Tick
        lblText.Left += direction

        ' Reverse direction when text reaches form boundaries
        If lblText.Left + lblText.Width > Me.ClientSize.Width Then
            direction = -1
        Else If lblText.Left < 0 Then
            direction = 1
        End If
    End Sub
End Class


Run the Program:

Press F5 or click Start Debugging button in Visual Studio.

Solution (VB.Net):

Public Class Form1
    Dim direction As Integer = 1 ' 1 for right, -1 for left

    Private Sub tmrMoveText_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles tmrMoveText.Tick
        lblText.Left += direction

        ' Reverse direction when text reaches form boundaries
        If lblText.Left + lblText.Width > Me.ClientSize.Width Then
            direction = -1
        Else If lblText.Left < 0 Then
            direction = 1
        End If
    End Sub
End Class
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Vb.net
IGNORE_WHEN_COPYING_END

B) C#.Net Program to Create Department Hierarchy:

Steps to Run on Visual Studio 2010:

Open Visual Studio 2010: Launch Visual Studio 2010.

Create New Project:

Go to File -> New -> Project....

In the New Project dialog:

Under Installed Templates, select Visual C#.

Choose Console Application.

Give a Name (e.g., DepartmentHierarchy) and Location for your project.

Click OK.

Write the Code:

Open Program.cs file in the Solution Explorer.

Replace the existing code with the following C# code:

using System;

namespace DepartmentHierarchy
{
    // Base class
    class Department
    {
        public string DepartmentName { get; set; }
        public int DepartmentID { get; set; }

        public virtual void AcceptDetails()
        {
            Console.Write("Enter Department Name: ");
            DepartmentName = Console.ReadLine();
            Console.Write("Enter Department ID: ");
            if (int.TryParse(Console.ReadLine(), out int id))
            {
                DepartmentID = id;
            }
            else
            {
                Console.WriteLine("Invalid ID format. Setting ID to 0.");
                DepartmentID = 0;
            }
        }

        public virtual void DisplayDetails()
        {
            Console.WriteLine($"Department Name: {DepartmentName}");
            Console.WriteLine($"Department ID: {DepartmentID}");
        }
    }

    // Derived class Sales
    class Sales : Department
    {
        public double TargetRevenue { get; set; }

        public override void AcceptDetails()
        {
            base.AcceptDetails(); // Call base class method first
            Console.Write("Enter Target Revenue for Sales Department: ");
            if (double.TryParse(Console.ReadLine(), out double revenue))
            {
                TargetRevenue = revenue;
            }
            else
            {
                Console.WriteLine("Invalid Revenue format. Setting Revenue to 0.");
                TargetRevenue = 0;
            }
        }

        public override void DisplayDetails()
        {
            Console.WriteLine("\n--- Sales Department Details ---");
            base.DisplayDetails(); // Call base class display
            Console.WriteLine($"Target Revenue: ${TargetRevenue}");
        }
    }

    // Derived class Human Resource
    class HumanResource : Department
    {
        public int EmployeeCount { get; set; }

        public override void AcceptDetails()
        {
            base.AcceptDetails(); // Call base class method first
            Console.Write("Enter Employee Count for HR Department: ");
            if (int.TryParse(Console.ReadLine(), out int count))
            {
                EmployeeCount = count;
            }
            else
            {
                Console.WriteLine("Invalid Employee Count format. Setting Count to 0.");
                EmployeeCount = 0;
            }
        }

        public override void DisplayDetails()
        {
            Console.WriteLine("\n--- Human Resource Department Details ---");
            base.DisplayDetails(); // Call base class display
            Console.WriteLine($"Employee Count: {EmployeeCount}");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Sales salesDept = new Sales();
            HumanResource hrDept = new HumanResource();

            Console.WriteLine("Enter Details for Sales Department:");
            salesDept.AcceptDetails();

            Console.WriteLine("\nEnter Details for Human Resource Department:");
            hrDept.AcceptDetails();

            salesDept.DisplayDetails();
            hrDept.DisplayDetails();

            Console.ReadKey(); // Pause to see output
        }
    }
}
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
C#
IGNORE_WHEN_COPYING_END

Run the Program:

Press Ctrl + F5 (Start Without Debugging) or F5 (Start Debugging) to run the program.

The program will prompt you to enter details for Sales and HR departments, and then display the entered details.

Solution (C#.Net):

using System;

// Base class
class Department
{
    public string DepartmentName { get; set; }
    public int DepartmentID { get; set; }

    public virtual void AcceptDetails() { /* ... */ }
    public virtual void DisplayDetails() { /* ... */ }
}

// Derived class Sales
class Sales : Department
{
    public double TargetRevenue { get; set; }
    public override void AcceptDetails() { /* ... */ }
    public override void DisplayDetails() { /* ... */ }
}

// Derived class Human Resource
class HumanResource : Department
{
    public int EmployeeCount { get; set; }
    public override void AcceptDetails() { /* ... */ }
    public override void DisplayDetails() { /* ... */ }
}

class Program
{
    static void Main(string[] args)
    {
        Sales salesDept = new Sales();
        HumanResource hrDept = new HumanResource();

        salesDept.AcceptDetails();
        hrDept.AcceptDetails();

        salesDept.DisplayDetails();
        hrDept.DisplayDetails();

        Console.ReadKey();
    }
}
