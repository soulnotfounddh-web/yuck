Ex-1

import java.util.Arrays;
public class SortCommandLine {
public static void main(String[] args) {

if (args.length == 0) {
System.out.println("Please provide some
integers as command
line arguments.");
return;
}

int[] numbers = new int[args.length];

for (int i = 0; i < args.length; i++) {
numbers[i] = Integer.parseInt(args[i]);
}

Arrays.sort(numbers);

System.out.println("Sorted numbers in
ascending order:");
for (int num : numbers) {
System.out.print(num + " ");
}
System.out.println();
}
}

OUTPUT:
javac SortCommandLine.java
java SortCommandLine 5 2 9 1 7



Ex-2

// Thread class
class MessageThread extends Thread {
    private String message;
    private int delay; // in milliseconds
    MessageThread(String message, int delay) {
        this.message = message;
        this.delay = delay;
    }
    public void run() {
        for (int i = 1; i <= 5; i++) { // print 5 times
            System.out.println(message);
            try {
                Thread.sleep(delay);
            } catch (InterruptedException e) {
                System.out.println("Thread interrupted");
            }
        }
    }
}


public class ThreeThreadsDemo {
    public static void main(String[] args) {
        MessageThread t1 = new MessageThread("Good Morning", 1000);
        MessageThread t2 = new MessageThread("Hello", 2000);
        MessageThread t3 = new MessageThread("Welcome", 3000);
        t1.start();
        t2.start();
        t3.start();
    }
}


Ex-3

class InvalidInputException extends Exception {
    public InvalidInputException(String message) {
        super(message);
    }
}

public class SafeDivision {
    public static void main(String[] args) {
        try {
            // Check number of arguments
            if (args.length != 2) {
                throw new InvalidInputException(
                    "Please provide exactly two integers x and y."
                );
            }
            int x, y;
            try {
                x = Integer.parseInt(args[0]);
                y = Integer.parseInt(args[1]);
            } catch (NumberFormatException e) {
                throw new InvalidInputException(
                    "Both x and y must be valid signed integers."
                );
            }
            if (y == 0) {
                throw new InvalidInputException(
                    "Division by zero is not allowed. y must not be zero."
                );
            }
            int result = x / y;
            System.out.println("x = " + x + ", y = " + y);
            System.out.println("Result of x / y = " + result);
        } catch (InvalidInputException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}

Ex-4

import java.io.*;

public class FileStats {
    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("Usage: java FileStats <filename>");
            return;
        }
        String fileName = args[0];
        int lineCount = 0;
        int wordCount = 0;
        int charCount = 0;
        try {
            BufferedReader br = new BufferedReader(new FileReader(fileName));
            String line;
            while ((line = br.readLine()) != null) {
                lineCount++;          
                charCount += line.length();
                String trimmed = line.trim();
                if (!trimmed.isEmpty()) {
                    String[] words = trimmed.split("\\s+");
                    wordCount += words.length;
                }
            }
            br.close();
            System.out.println("File Name : " + fileName);
            System.out.println("Lines : " + lineCount);
            System.out.println("Words : " + wordCount);
            System.out.println("Characters : " + charCount);
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + fileName);
        } catch (IOException e) {
            System.out.println("Error reading file.");
        }
    }
}


Ex-5

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class FactorialSwing extends JFrame implements ActionListener {
   JTextField inputField, outputField;
    JButton computeButton;
    public FactorialSwing() {
        setTitle("Factorial Calculator");
        setSize(350, 180);
        setLayout(new FlowLayout());
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        add(new JLabel("Enter Number:"));
        inputField = new JTextField(10);
        add(inputField);
        add(new JLabel("Factorial:"));
        outputField = new JTextField(10);
        outputField.setEditable(false);
        add(outputField);
        computeButton = new JButton("Compute");
        computeButton.addActionListener(this);
        add(computeButton);
        setVisible(true);
    }
    public void actionPerformed(ActionEvent e) {
        try {
            int n = Integer.parseInt(inputField.getText());
            if (n < 0) {
                outputField.setText("Invalid");
                return;
            }
            long fact = 1;
            for (int i = 1; i <= n; i++) {
                fact *= i;
            }
            outputField.setText(Long.toString(fact));
        } catch (NumberFormatException ex) {
            outputField.setText("Invalid");
        }
    }
    public static void main(String[] args) {
        new FactorialSwing();
    }
}


Ex-6

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class AdvancedJavaLabGUI extends JFrame implements ActionListener {
    JCheckBox cbJava, cbPython, cbDBMS, cbWeb;
    JRadioButton rbMale, rbFemale, rbOther;
    ButtonGroup genderGroup;
    JButton btnShow, btnClear, btnExit;
    JTextArea displayArea;
    public AdvancedJavaLabGUI() {
        setTitle("Advanced Java Lab I MCA – Course Selection");
        setSize(600, 420);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout(10, 10));
        JLabel header = new JLabel("ADVANCED JAVA LAB I MCA", JLabel.CENTER);
        header.setFont(new Font("Arial", Font.BOLD, 22));
        add(header, BorderLayout.NORTH);
        JPanel leftPanel = new JPanel();
        leftPanel.setLayout(new GridLayout(2, 1, 10, 10));
        JPanel coursePanel = new JPanel(new GridLayout(5, 1, 5, 5));
        coursePanel.setBorder(BorderFactory.createTitledBorder("Select Courses"));
        cbJava = new JCheckBox("Java");
        cbPython = new JCheckBox("Python");
        cbDBMS = new JCheckBox("DBMS");
        cbWeb = new JCheckBox("Web Development");
        coursePanel.add(new JLabel("Courses:"));
        coursePanel.add(cbJava);
        coursePanel.add(cbPython);
        coursePanel.add(cbDBMS);
        coursePanel.add(cbWeb);
        JPanel genderPanel = new JPanel(new GridLayout(4, 1, 5, 5));
        genderPanel.setBorder(BorderFactory.createTitledBorder("Select Gender"));
        rbMale = new JRadioButton("Male");
        rbFemale = new JRadioButton("Female");
        rbOther = new JRadioButton("Other");
        genderGroup = new ButtonGroup();
        genderGroup.add(rbMale);
        genderGroup.add(rbFemale);
        genderGroup.add(rbOther);
        genderPanel.add(new JLabel("Gender:"));
        genderPanel.add(rbMale);
        genderPanel.add(rbFemale);
        genderPanel.add(rbOther);
        leftPanel.add(coursePanel);
        leftPanel.add(genderPanel);
        add(leftPanel, BorderLayout.WEST);
        displayArea = new JTextArea();
        displayArea.setFont(new Font("Consolas", Font.PLAIN, 14));
        displayArea.setEditable(false);
        displayArea.setBorder(BorderFactory.createTitledBorder("Selected Details"));
        JScrollPane sp = new JScrollPane(displayArea);
        add(sp, BorderLayout.CENTER);
        displayArea.setText("=== Advanced Java Lab I MCA 2025 Batch ===\n\n");
        JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 15, 10));
        btnShow = new JButton("Show Selection");
        btnClear = new JButton("Clear");
        btnExit = new JButton("Exit");
        btnShow.addActionListener(this);
        btnClear.addActionListener(this);
        btnExit.addActionListener(this);
        buttonPanel.add(btnShow);
        buttonPanel.add(btnClear);
        buttonPanel.add(btnExit);
        add(buttonPanel, BorderLayout.SOUTH);
        setVisible(true);
    }
    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == btnShow) {
            StringBuilder courses = new StringBuilder();
            if (cbJava.isSelected()) courses.append("Java, ");
            if (cbPython.isSelected()) courses.append("Python, ");
            if (cbDBMS.isSelected()) courses.append("DBMS, ");
            if (cbWeb.isSelected()) courses.append("Web Development, ");
            String selectedCourses = courses.length() > 0
                    ? courses.substring(0, courses.length() - 2)
                    : "No course selected";
            String gender = "Not selected";
            if (rbMale.isSelected()) gender = "Male";
            else if (rbFemale.isSelected()) gender = "Female";
            else if (rbOther.isSelected()) gender = "Other";
            displayArea.setText("=== Advanced Java Lab I MCA 2025 Batch ===\n\n");
            displayArea.append("Selected Courses : " + selectedCourses + "\n");
            displayArea.append("Selected Gender : " + gender + "\n");
        }
        else if (e.getSource() == btnClear) {
            cbJava.setSelected(false);
            cbPython.setSelected(false);
            cbDBMS.setSelected(false);
            cbWeb.setSelected(false);
            genderGroup.clearSelection();
            displayArea.setText("=== Advanced Java Lab I MCA 2025 Batch ===\n\n");
            displayArea.append("Cleared selections.\n");
        }
        else if (e.getSource() == btnExit) {
            System.exit(0);
        }
    }
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new AdvancedJavaLabGUI());
    }
}


Ex-7

CREATE DATABASE IF NOT EXISTS library_db;

USE library_db;

CREATE TABLE IF NOT EXISTS books (
    book_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL,
    author VARCHAR(100) NOT NULL,
    price DOUBLE NOT NULL,
    publisher VARCHAR(100) NOT NULL
);


import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class LibraryInsert {
    private static final String URL = "jdbc:mysql://localhost:3306/library_db";
    private static final String USER = "root";
    private static final String PASS = "root"; // put your MySQL password here
    public static void main(String[] args) {
        String title = "Java Programming";
        String author = "Herbert Schildt";
        double price = 550.00;
        String publisher = "McGraw Hill";
        String sql = "INSERT INTO books(title, author, price, publisher) VALUES (?, ?, ?, ?)";
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            try (
                Connection con = DriverManager.getConnection(URL, USER, PASS);
                PreparedStatement ps = con.prepareStatement(sql)
            ) {
                ps.setString(1, title);
                ps.setString(2, author);
                ps.setDouble(3, price);
                ps.setString(4, publisher);
                int rows = ps.executeUpdate();
                if (rows > 0) {
                    System.out.println("Book inserted successfully!");
                } else {
                    System.out.println("Insert failed!");
                }
            }
        } catch (ClassNotFoundException e) {
            System.out.println("JDBC Driver not found. Add mysql-connector-j jar.");
        } catch (SQLException e) {
            System.out.println("Database error: " + e.getMessage());
        }
    }
}


Ex-8

NOT AVAILABLE


EX-9

package com.demo;

import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(name = "MyCookieServlet", urlPatterns = {"/makecookie"})
public class MyCookieServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        Cookie c = new Cookie("user", "Student");
        c.setMaxAge(300);
        response.addCookie(c);
        try (PrintWriter out = response.getWriter()) {
            out.println("<!DOCTYPE html>");
            out.println("<html>");
            out.println("<head><title>Cookie Page</title></head>");
            out.println("<body>");
            out.println("<h1>Success!</h1>");
            out.println("<p>A cookie named <b>'user'</b> has been created.</p>");
            out.println("<p>It will expire in 5 minutes.</p>");
            out.println("</body>");
            out.println("</html>");
        }
    }
}


Ex-10

<!DOCTYPE html>
<html>
<head>
    <title>Login Page</title>
</head>
<body>
    <h2>Login to System</h2>
    <form action="LoginServlet" method="POST">
        Username: <input type="text" name="txtUser"><br><br>
        Password: <input type="password" name="txtPass"><br><br>
        <input type="submit" value="Login">
    </form>

</body>
</html>

package com.auth;

import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(name = "LoginServlet", urlPatterns = {"/LoginServlet"})
public class LoginServlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        String user = request.getParameter("txtUser");
        String pass = request.getParameter("txtPass");
        try (PrintWriter out = response.getWriter()) {
            out.println("<html><body>");
            if ("admin".equals(user) && "12345".equals(pass)) {
                out.println("<h1>Welcome, " + user + "!</h1>");
                out.println("<p>Login Successful.</p>");
            } else {
                out.println("<h1 style='color:red;'>Login Failed!</h1>");
                out.println("<p>Invalid username or password.</p>");
                out.println("<a href='login.html'>Try Again</a>");
            }
            out.println("</body></html>");
        }
    }
}

Ex-11

public class TestEmployee {
    public static void main(String[] args) {
        EmployeeBean emp = new EmployeeBean();
        emp.setName("Dr. Nithyanandh Selvam");
        emp.setSalary(75000);
        emp.setDesignation("Professor");
        emp.setCompany("PSG College of Arts & Science");
        System.out.println("Employee Details");
        System.out.println("-------------------------");
        System.out.println("Name: " + emp.getName());
        System.out.println("Salary: " + emp.getSalary());
        System.out.println("Designation: " + emp.getDesignation());
        System.out.println("Company: " + emp.getCompany());
    }
}

public class EmployeeBean {
    private String name;
    private double salary;
    private String designation;
    private String company;
    public EmployeeBean() {
    }
    public void setName(String name) {
        this.name = name;
    }
    public void setSalary(double salary) {
        this.salary = salary;
    }
    public void setDesignation(String designation) {
        this.designation = designation;
    }
    public void setCompany(String company) {
        this.company = company;
    }
    public String getName() {
        return name;
    }
    public double getSalary() {
        return salary;
    }
    public String getDesignation() {
        return designation;
    }
    public String getCompany() {
        return company;
    }
}


Ex-12

package com.demo;

import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(name = "CounterServlet", urlPatterns = {"/CounterServlet"})
public class CounterServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        PrintWriter out = response.getWriter();
        Cookie[] cookies = request.getCookies();
        int count = 0;
        if (cookies != null) {
            for (Cookie c : cookies) {
                if (c.getName().equals("visit_count")) {
                    count = Integer.parseInt(c.getValue());
                    break;
                }
            }
        }
        count++;
        Cookie counterCookie = new Cookie("visit_count", String.valueOf(count));
        counterCookie.setMaxAge(24 * 60 * 60);
        response.addCookie(counterCookie);
        out.println("<html><head><title>Visit Counter</title></head><body>");
        if (count == 1) {
            out.println("<h2>Welcome! This is your first visit.</h2>");
        } else {
            out.println("<h2>Welcome back!</h2>");
            out.println("<h3>You have visited this page " + count + " times.</h3>");
        }
        out.println("<p>Refresh the page to see the counter increase.</p>");
        out.println("</body></html>");
    }
}

