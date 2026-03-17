import java.util.Arrays;
public class SortCommandLine {
public static void main(String[] args) {
// Check if any numbers are passed
if (args.length == 0) {
System.out.println("Please provide some
integers as command
line arguments.");
return;
}
// Create an integer array
int[] numbers = new int[args.length];
// Convert String arguments to integers
for (int i = 0; i < args.length; i++) {
numbers[i] = Integer.parseInt(args[i]);
}
// Sort the array in ascending order
Arrays.sort(numbers);
// Display sorted numbers
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
Sorted numbers in ascending order:
1 2 5 7 9
EX-2
class MessageThread extends Thread {
private String message;
private int delay; // in milliseconds
MessageThread(String message, int delay)
{
this.message = message;
this.delay = delay;
}
public void run() {
for (int i = 1; i <= 5; i++) {
// print 5 times
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
MessageThread t1 = new
MessageThread("Good Morning", 1000);
MessageThread t2 = new
MessageThread("Hello", 2000);
MessageThread t3 = new
MessageThread("Welcome", 3000);
t1.start();
t2.start();
t3.start();
}
}
OUTPUT:
Good Morning
Hello
Welcome
Good Morning
Good Morning
Hello
Good Morning
Welcome
EX-3
// Custom exception class
class InvalidInputException extends
Exception {
public InvalidInputException(String
message) {
super(message);
}
}
public class SafeDivision {
public static void main(String[] args) {
try {
// Check number of arguments
if (args.length != 2) {
throw new InvalidInputException("Please
provide exactly two
integers x and y.");
}
int x, y;
try {
x = Integer.parseInt(args[0]);
y = Integer.parseInt(args[1]);
} catch (NumberFormatException e) {
throw new InvalidInputException("Both x
and y must be valid
signed integers.");
}
if (y == 0) {
throw new
InvalidInputException("Division by zero is
not
allowed. y must not be zero.");
}
int result = x / y;
System.out.println("x = " + x + ", y = " +
y);
System.out.println("Result of x / y = " +
result);
} catch (InvalidInputException e) {
System.out.println("Error: " +
e.getMessage());
}
}
}
OUTPUT:
javac SafeDivision.java
java SafeDivision 10 2
x = 10, y = 2
Result of x / y = 5
java SafeDivision 10 0
Error: Division by zero is not allowed. y
must not be zero.
java SafeDivision 10 abc
Error: Both x and y must be valid signed
integers.
EX-4
import java.io.*;
public class FileStats {
public static void main(String[] args) {
if (args.length != 1) {
System.out.println("Usage: java FileStats
<filename>");
return;
}
String fileName = args[0];
int lineCount = 0;
int wordCount = 0;
int charCount = 0;
try {
BufferedReader br = new
BufferedReader(new
FileReader(fileName));
String line;
while ((line = br.readLine()) != null) {
lineCount++;
// Count characters (without newline)
charCount += line.length();
// Count words
String trimmed = line.trim();
if (!trimmed.isEmpty()) {
String[] words = trimmed.split("\\s+");
wordCount += words.length;
}
}
br.close();
System.out.println("File Name : " +
fileName);
System.out.println("Lines : " + lineCount);
System.out.println("Words : " +
wordCount);
System.out.println("Characters : " +
charCount);
} catch (FileNotFoundException e) {
System.out.println("File not found: " +
fileName);
} catch (IOException e) {
System.out.println("Error reading file.");
}
}
}
OUTPUT:
java FileStats sample.txt (Text File Should
be in the Same Folder)
File Name : sample.txt
Lines : 2
Words : 4
Characters : 22
EX-5
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
public class FactorialSwing extends
JFrame implements ActionListener {
JTextField inputField, outputField;
JButton computeButton;
public FactorialSwing() {
setTitle("Factorial Calculator");
setSize(350, 180);
setLayout(new FlowLayout());
setDefaultCloseOperation(JFrame.EXIT_
ON_CLOSE);
// Input Label and Text field
add(new JLabel("Enter Number:"));
inputField = new JTextField(10);
add(inputField);
// Output Label and Text field
add(new JLabel("Factorial:"));
outputField = new JTextField(10);
outputField.setEditable(false);
add(outputField);
// Compute Button
computeButton = new
JButton("Compute");
computeButton.addActionListener(this);
add(computeButton);
setVisible(true);
}
public void actionPerformed(ActionEvent
e) {
try {
int n =
Integer.parseInt(inputField.getText());
if (n < 0) {
outputField.setText("Invalid");
return;
}
long fact = 1;
for (int i = 1; i <= n; i++)
fact *= i;
outputField.setText(Long.toString(fact));
} catch (NumberFormatException ex) {
outputField.setText("Invalid");
public static void main(String[] args) {
new FactorialSwing();
}
}
}
}
OUTPUT:
// Radio Buttons (Gender)
JRadioButton rbMale, rbFemale, rbOther;
ButtonGroup genderGroup;
// Buttons + TextArea
JButton btnShow, btnClear, btnExit;
JTextArea displayArea;
public AdvancedJavaLabGUI() {
setTitle("Advanced Java Lab I MCA –
Course Selection");
setSize(600, 420);
setLocationRelativeTo(null);
EX-6
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
public class AdvancedJavaLabGUI
extends JFrame implements
ActionListener {
// Checkboxes (Courses)
JCheckBox cbJava, cbPython, cbDBMS,
cbWeb;
setDefaultCloseOperation(JFrame.EXIT_
ON_CLOSE);
setLayout(new BorderLayout(10, 10));
// Top Header
JLabel header = new
JLabel("ADVANCED JAVA LAB I
MCA", JLabel.CENTER);
header.setFont(new Font("Arial",
Font.BOLD, 22));
add(header, BorderLayout.NORTH);
// Left Panel (Inputs)
JPanel leftPanel = new JPanel();
leftPanel.setLayout(new GridLayout(2, 1,
10, 10));
// Courses Panel
JPanel coursePanel = new JPanel(new
GridLayout(5, 1, 5, 5));
coursePanel.setBorder(BorderFactory.creat
eTitledBorder("Select
Courses"));
cbJava = new JCheckBox("Java");
cbPython = new JCheckBox("Python");
cbDBMS = new JCheckBox("DBMS");
cbWeb = new JCheckBox("Web
Development");
coursePanel.add(new JLabel("Courses:"));
coursePanel.add(cbJava);
coursePanel.add(cbPython);
coursePanel.add(cbDBMS);
coursePanel.add(cbWeb);
// Gender Panel
JPanel genderPanel = new JPanel(new
GridLayout(4, 1, 5, 5));
genderPanel.setBorder(BorderFactory.crea
teTitledBorder("Select Gender"));
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
// Center Panel (TextArea)
displayArea = new JTextArea();
displayArea.setFont(new Font("Consolas",
Font.PLAIN, 14));
displayArea.setEditable(false);
displayArea.setBorder(BorderFactory.creat
eTitledBorder("Selected
Details"));
JScrollPane sp = new
JScrollPane(displayArea);
add(sp, BorderLayout.CENTER);
// Put title inside TextArea (as requested)
displayArea.setText("=== Advanced Java
Lab I MCA 2025 Batch ===\n\n");
// Bottom Panel (Buttons)
JPanel buttonPanel = new JPanel(new
FlowLayout(FlowLayout.CENTER, 15,
10));
btnShow = new JButton("Show
Selection");
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
public void actionPerformed(ActionEvent
e) {
if (e.getSource() == btnShow) {
StringBuilder courses = new
StringBuilder();
if (cbJava.isSelected())
courses.append("Java, ");
if (cbPython.isSelected())
courses.append("Python, ");
if (cbDBMS.isSelected())
courses.append("DBMS, ");
if (cbWeb.isSelected())
courses.append("Web Development, ");
// condition ? value_if_true : value_if_false
String selectedCourses = courses.length()
> 0
? courses.substring(0, courses.length() - 2)
// remove last ", "
: "No course selected";
String gender = "Not selected";
if (rbMale.isSelected()) gender = "Male";
else if (rbFemale.isSelected()) gender =
"Female";
else if (rbOther.isSelected()) gender =
"Other";
displayArea.setText("=== Advanced Java
Lab I MCA 2025 Batch ===\n\n");
displayArea.append("Selected Courses : "
+ selectedCourses + "\n");
displayArea.append("Selected Gender : " +
gender + "\n");
}
cbPython.setSelected(false);
cbDBMS.setSelected(false);
cbWeb.setSelected(false);
genderGroup.clearSelection();
displayArea.setText("=== Advanced Java
Lab I MCA 2025 Batch ===\n\n");
displayArea.append("Cleared
selections.\n");
}
else if (e.getSource() == btnExit) {
System.exit(0);
}
}
public static void main(String[] args) {
// Run GUI safely
SwingUtilities.invokeLater(() -> new
AdvancedJavaLabGUI());
}}
OUTPUT:
else if (e.getSource() == btnClear) {
cbJava.setSelected(false);
