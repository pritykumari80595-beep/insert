import java.sql.*;
import java.util.Scanner;

public class pre11 {
    public static void main(String[] args) {

        String url = "jdbc:mysql://localhost:3306/college";
        String user = "root";
        String password = "root";
        String query = "insert into student(id,name,marks) values (?,?,?)";

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            System.out.println("Driver Loaded");

            Connection connection = DriverManager.getConnection(url, user, password);
            System.out.println("Connection Established");

            PreparedStatement ps = connection.prepareStatement(query);
            System.out.println("Statement Created");

            Scanner sc = new Scanner(System.in);

            for (int i = 1; i <= 3; i++) {

                System.out.println("Enter id:");
                int id = sc.nextInt();

                System.out.println("Enter name:");
                String name = sc.next();

                System.out.println("Enter marks:");
                int marks = sc.nextInt();

                ps.setInt(1, id);
                ps.setString(2, name);
                ps.setInt(3, marks);

                ps.executeUpdate();   
            }

            System.out.println("All records inserted successfully!");

            ps.close();
            connection.close();
            sc.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
