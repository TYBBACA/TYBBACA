
1. PrimeServer.java (Server-side)

import java.net.*;
import java.io.*;

public class PrimeServer {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(5000)) { // Port number 5000
            System.out.println("Server is running and waiting for client...");

            while (true) {
                Socket clientSocket = serverSocket.accept();
                System.out.println("Client connected: " + clientSocket);

                try (
                    PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);
                    BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
                ) {
                    String inputLine;
                    while ((inputLine = in.readLine()) != null) {
                        try {
                            int number = Integer.parseInt(inputLine);
                            boolean isPrime = isPrime(number);
                            out.println(isPrime ? "Prime" : "Not Prime");
                        } catch (NumberFormatException e) {
                            out.println("Invalid Input. Please send a number.");
                        }
                        break; // Process one number per connection
                    }
                } catch (IOException e) {
                    System.out.println("Exception in handling client: " + e.getMessage());
                } finally {
                    clientSocket.close();
                    System.out.println("Client disconnected: " + clientSocket);
                }
            }
        } catch (IOException e) {
            System.out.println("Could not listen on port 5000: " + e.getMessage());
        }
    }

    public static boolean isPrime(int n) {
        if (n <= 1) return false;
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) return false;
        }
        return true;
    }
}


2. PrimeClient.java (Client-side)

import java.net.*;
import java.io.*;
import java.util.Scanner;

public class PrimeClient {
    public static void main(String[] args) {
        String serverAddress = "127.0.0.1"; // Localhost
        int port = 5000;

        try (
            Socket socket = new Socket(serverAddress, port);
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            Scanner scanner = new Scanner(System.in)
        ) {
            System.out.println("Connected to server.");

            System.out.print("Enter a number to check for prime: ");
            String number = scanner.nextLine();
            out.println(number);

            String response = in.readLine();
            System.out.println("Server response: " + response);

        } catch (IOException e) {
            System.out.println("Client Exception: " + e.getMessage());
        }
    }
}


Question B: Bouncing Ball Applet with Random Colors

Solution:

Here is the Java Applet program (BouncingBallApplet.java).

import java.applet.Applet;
import java.awt.*;
import java.util.Random;

public class BouncingBallApplet extends Applet implements Runnable {
    private int x, y, radius;
    private int dx, dy;
    private Color ballColor;
    private Thread animator;
    private Random random;

    @Override
    public void init() {
        setSize(300, 200); // Set applet size
        x = 50;
        y = 50;
        radius = 20;
        dx = 2;
        dy = 3;
        random = new Random();
        changeColor(); // Initial color
    }

    @Override
    public void start() {
        animator = new Thread(this);
        animator.start();
    }

    @Override
    public void stop() {
        animator = null;
    }

    @Override
    public void paint(Graphics g) {
        g.clearRect(0, 0, getWidth(), getHeight()); // Clear background
        g.setColor(ballColor);
        g.fillOval(x - radius, y - radius, 2 * radius, 2 * radius);
    }

    @Override
    public void run() {
        Thread currentThread = Thread.currentThread();
        while (currentThread == animator) {
            x += dx;
            y += dy;

            // Bounce off walls
            if (x - radius < 0 || x + radius > getWidth()) {
                dx = -dx;
                changeColor(); // Change color on bounce
            }
            if (y - radius < 0 || y + radius > getHeight()) {
                dy = -dy;
                changeColor(); // Change color on bounce
            }

            repaint(); // Request repaint
            try {
                Thread.sleep(30); // Animation speed (milliseconds)
            } catch (InterruptedException e) {
                break;
            }
        }
    }

    private void changeColor() {
        ballColor = new Color(random.nextInt(256), random.nextInt(256), random.nextInt(256));
    }
}

Steps to Run Question B:

Save: Save the code as BouncingBallApplet.java.

Compile: Open a command prompt or terminal and navigate to the directory where you saved the file. Compile using:

javac BouncingBallApplet.java
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Cmd
IGNORE_WHEN_COPYING_END

Create HTML file: Create a new text file named ball.html in the same directory and paste the following HTML code:

<html>
<head>
    <title>Bouncing Ball Applet</title>
</head>
<body>
    <applet code="BouncingBallApplet.class" width="300" height="200">
    </applet>
</body>
</html>
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Html
IGNORE_WHEN_COPYING_END

Run Applet:

Using Appletviewer (JDK tool): Open a command prompt/terminal in the same directory and run:

appletviewer ball.html
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Cmd
IGNORE_WHEN_COPYING_END

Using a Web Browser: Open the ball.html file in a web browser that supports Java Applets (Note: Modern browsers may have disabled or deprecated Java Applet support. If your browser doesn't run it, use appletviewer).

You should see a window with a bouncing ball that changes color every time it hits a wall.

These are short and clear solutions with steps to run them on your command prompt. Let me know if you have any other questions!


Okay, let's solve both parts of Question Q.2 step-by-step.

Question A: C# .NET Program for Sum of Two Numbers

Solution:

Here is the C# .NET program (SumNumbers.cs).

using System;

public class SumNumbers
{
    public static int SumOfTwoNumbers(int num1, int num2)
    {
        return num1 + num2;
    }

    public static void Main(string[] args)
    {
        Console.WriteLine("Enter the first number:");
        int number1 = Convert.ToInt32(Console.ReadLine());

        Console.WriteLine("Enter the second number:");
        int number2 = Convert.ToInt32(Console.ReadLine());

        int sum = SumOfTwoNumbers(number1, number2);
        Console.WriteLine("The sum of " + number1 + " and " + number2 + " is: " + sum);

        Console.ReadKey(); // To keep the console window open until a key is pressed
    }
}

Question B: VB.NET Program for Teacher Table

Solution:

Here is the VB.NET program (TeacherTable.vb).

Module TeacherModule

    Class Teacher
        Public Tid As Integer
        Public TName As String
        Public Subject As String

        Public Sub New(tid As Integer, tname As String, subject As String)
            Me.Tid = tid
            Me.TName = tname
            Me.Subject = subject
        End Sub
    End Class

    Sub Main()
        Dim teachers As New List(Of Teacher)()

        ' Insert records
        teachers.Add(New Teacher(1, "Seeta", "Math"))
        teachers.Add(New Teacher(2, "Geeta", "Science"))
        teachers.Add(New Teacher(3, "Rita", "English"))
        teachers.Add(New Teacher(4, "Mita", "History"))
        teachers.Add(New Teacher(5, "Nita", "Computer"))


        ' Search for teacher named "Seeta"
        Dim searchName As String = "Seeta"
        Dim foundTeacher As Teacher = teachers.Find(Function(t) t.TName.Equals(searchName, StringComparison.OrdinalIgnoreCase))

        If foundTeacher IsNot Nothing Then
            Console.WriteLine("Teacher found:")
            Console.WriteLine("Tid: " & foundTeacher.Tid)
            Console.WriteLine("TName: " & foundTeacher.TName)
            Console.WriteLine("Subject: " & foundTeacher.Subject)
        Else
            Console.WriteLine("Teacher named '" & searchName & "' not found.")
        End If

        Console.ReadKey() ' To keep the console window open
    End Sub

End Module
