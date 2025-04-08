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
