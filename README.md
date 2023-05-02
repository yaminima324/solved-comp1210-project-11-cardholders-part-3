Download Link: https://assignmentchef.com/product/solved-comp1210-project-11-cardholders-part-3
<br>
Cardholders – Part 3 is the third of a three-part software project to process the monthly purchases made by Sapphire, Diamond, and Blue Diamond cardholders.

The completed class hierarchy is shown in the UML class diagram at right.  Part 3 of the project focuses on handling exceptions that are thrown as a result of erroneous input from the command line or the data file.  The main method in the CardholdersPart3App class, which reads in the file name from the command line, will need handle a

FileNotFoundException that may result from

attempting to open the file (e.g., if the file does not exist).  Also, the readCardholderFile method in CardholderProcessor will need to handle exceptions that occur while processing the data file, including a new exception called InvalidCategoryException.

<strong> </strong>

<strong>Cardholder, SapphireCardholder, DiamondCardholder, BlueDiamondCardholder, CurrentBalanceComparator</strong>

<strong> </strong>

<strong>Requirements and Design:</strong>  There are no changes to these classes from Part 2.

<strong> </strong>

<h1><strong>CardholderProcessor.java </strong></h1>

<strong> </strong>

<strong>Requirements: </strong>The CardholderProcessor class provides methods for reading in the data file and generating the monthly report.  The readCardholderFile method should redesigned to handle exceptions in the data.  A “good” line of data results in a new element added the Cardholder array, and “bad” line of data results in the line + exception message being added the to the invalid records array.  A new report method produces the Invalid Records Report.




<strong>Design: </strong>The readCardholderFile method from Part 2 should be redesigned to handle exceptions.

CardholderProcessor class has fields, a constructor, and methods as outlined below.

<ul>

 <li><strong>Fields:</strong> no change from Part 2.</li>

 <li><strong>Constructor: </strong>no change from Part 2.</li>

 <li><strong>Methods:</strong> The readCardholderFile needs to be reworked and the generateInvalidRecordsReport method needs to be added. <u>See Part 2 for the full description of other methods in this class</u>. o readCardholderFile has no return value, accepts the data file name as a String, and throws FileNotFoundException.  If a FileNotFoundException occurs when attempting to open the data file, it should be ignored in this method so that it can be handled in the calling method (i.e., main).  If a line from the file is processed successfully, a Cardholder object of the appropriate category (subclass) is added to the Cardholder array field.  However, when an exception occurs as a result from erroneous data in a line read from the file, it should be caught and handled as follows.  The exception message should be concatenated to the line and then the resulting String should be added to the invalid records array field in the class.  The two exceptions that should be caught in this method are the InvalidCategoryException (described below) and the NumberFormatException.   Note that the InvalidCategoryException must be explicitly thrown by your code if the category is not 1, 2, or 3; whereas, the</li>

</ul>

NumberFormatException will be thrown automatically if the item scanned in the line from the file is not a double when Double.parseDouble expects it to be a double.

o generateInvalidRecordsReport processes the invalid records array to produce the Invalid Records Report and then returns the report as String.  See the example result near the end of the output for CardholdersPart3App that begins on page 4 and ends on page 6.




<strong>Code and Test:  </strong>See examples of exception handling in the text and the class notes.  Download cardholder_data_3_exceptions.txt from the assignment page in Canvas to test your program. Your JUnit test methods should force the exceptions described above to thrown and caught.

Since the readCardholderFile method will propagate the FileNotFoundException if the file is not found when the Scanner is created to read the file, your test method could catch this exception to check that it was thrown.  <strong> </strong>

<strong> </strong>

<h1><strong>InvalidCategoryException.java </strong></h1>

<strong> </strong>

<strong>Requirements and Design: </strong>The InvalidCategoryException class defines a new subclass of the Exception class.  The constructor invokes the super constructor with the message: “*** invalid category ***”.  See examples of creating user defined in from text and class notes.




<h1><strong>CardholdersPart3App.java </strong></h1>

<strong> </strong>

<strong>Requirements: </strong>The CardholdersPart3App class contains the main method for running the program. In addition to the specifications in Part 2, the main method should be modified as indicated below.




<strong>Design: </strong>The CardholdersPart3App class is the driver class and has a main method described below.




o main accepts a file name as a command line argument, then within a try block, creates a CardholderProcessor object,  and then invokes its methods to read the file and process the reward records and then to generate and print the <u>four reports</u> as shown in the example output beginning on page 4.  If no command line argument is provided, the program should indicate this and end as shown in the first example output on page 4.  If an FileNotFoundException is thrown in the readCardholderFile method in the CardholderProcessor class, it should be caught in the catch block of the try statement.  The catch block should print a message (“***

Attempted to read file: ” along with the exception’s message).  For example, if the user entered “nofile.txt” as the command line argument and this file does not exit, then the Run I/O in jGRASP would look like the following (this is also repeated in the example output beginning on page 4).  Note that since the main method is catching FileNotFoundException, it no longer needs the throws clause in its declaration.




MM«M —-jGRASP exec: java CardholdersPart3App nofile.txt

MM§M *** Attempted to read file: nofile.txt (No such file or directory) MM§M

MM©M —-jGRASP: operation complete.










<strong>Code and Test:  </strong>See examples of exception handling in the text and the class notes.  Download cardholder_data_3_exceptions.txt from the assignment page in Canvas to test your program.  One of your JUnit test methods should call your main method with an argument this is <u>not</u> a valid file name to ensure that your catch block is covered.  See “Code and Test” for

CardholdersPart2App in Part 2 to see how to invoke your main method.<strong>                         </strong>

<h1><strong>Example Output  </strong></h1>




Three separate runs are shown below: (1) one with no command line argument, (2) one with an invalid file name as command line argument, and (3) one with valid file name as command line argument.




<strong> </strong>

<table width="639">

 <tbody>

  <tr>

   <td width="639">MM«M —-jGRASP exec: java CardholdersPart3App MM§MFile name expected as command line argument. MM§MProgram ending.MM§MMM©M —-jGRASP: operation complete.MM«M —-jGRASP exec: java CardholdersPart3App nofile.txtMM§M *** Attempted to read file: nofile.txt (No such file or directory)MM§MMM©M —-jGRASP: operation complete. MM«M —-jGRASP exec: java CardholdersPart3App cardholder_data_3_exceptions.txtMM§M—————————- MM§MMonthly Cardholder ReportMM§M—————————-MM§MDiamond CardholderMM§MAcctNo/Name: 10002 Jones, PatMM§MPrevious Balance: $1,200.00MM§MPayment: ($100.00)MM§MInterest: $11.00MM§MNew Purchases: $473.10MM§MCurrent Balance: $1,584.10MM§MMinimum Payment: $47.52MM§MPurchase Points: 1,419MM§M(includes 5.0% discount rate applied to New Purchases)MM§MMM§MBlue Diamond CardholderMM§MAcctNo/Name: 10003 King, KellyMM§MPrevious Balance: $1,300.00MM§MPayment: ($150.00)MM§MInterest: $11.50MM§MNew Purchases: $538.20MM§MCurrent Balance: $1,699.70MM§MMinimum Payment: $50.99MM§MPurchase Points: 2,690MM§M(includes 10.0% discount rate applied to New Purchases)MM§MMM§MSapphire CardholderMM§MAcctNo/Name: 10001 Smith, SamMM§MPrevious Balance: $1,100.00MM§MPayment: ($200.00)MM§MInterest: $9.00MM§MNew Purchases: $548.00MM§MCurrent Balance: $1,457.00MM§MMinimum Payment: $43.71MM§MPurchase Points: 548 MM§MMM§MBlue Diamond CardholderMM§MAcctNo/Name: 10004 Jenkins, JordanMM§MPrevious Balance: $1,400.00MM§MPayment: ($1,400.00)MM§MInterest: $0.00</td>

  </tr>

 </tbody>

</table>




<table width="639">

 <tbody>

  <tr>

   <td width="639">MM§MNew Purchases: $9,000.00MM§MCurrent Balance: $9,000.00MM§MMinimum Payment: $270.00MM§MPurchase Points: 47,500MM§M(includes 10.0% discount rate applied to New Purchases)MM§M(includes 2,500 bonus points added to Purchase Points)MM§MMM§M————————————– MM§MMonthly Cardholder Report (by Name)MM§M————————————–MM§MBlue Diamond CardholderMM§MAcctNo/Name: 10004 Jenkins, JordanMM§MPrevious Balance: $1,400.00MM§MPayment: ($1,400.00)MM§MInterest: $0.00MM§MNew Purchases: $9,000.00MM§MCurrent Balance: $9,000.00MM§MMinimum Payment: $270.00MM§MPurchase Points: 47,500MM§M(includes 10.0% discount rate applied to New Purchases)MM§M(includes 2,500 bonus points added to Purchase Points)MM§MMM§MDiamond CardholderMM§MAcctNo/Name: 10002 Jones, PatMM§MPrevious Balance: $1,200.00MM§MPayment: ($100.00)MM§MInterest: $11.00MM§MNew Purchases: $473.10MM§MCurrent Balance: $1,584.10MM§MMinimum Payment: $47.52MM§MPurchase Points: 1,419MM§M(includes 5.0% discount rate applied to New Purchases)MM§MMM§MBlue Diamond CardholderMM§MAcctNo/Name: 10003 King, KellyMM§MPrevious Balance: $1,300.00MM§MPayment: ($150.00)MM§MInterest: $11.50MM§MNew Purchases: $538.20MM§MCurrent Balance: $1,699.70MM§MMinimum Payment: $50.99MM§MPurchase Points: 2,690MM§M(includes 10.0% discount rate applied to New Purchases)MM§MMM§MSapphire CardholderMM§MAcctNo/Name: 10001 Smith, SamMM§MPrevious Balance: $1,100.00MM§MPayment: ($200.00)MM§MInterest: $9.00MM§MNew Purchases: $548.00MM§MCurrent Balance: $1,457.00MM§MMinimum Payment: $43.71MM§MPurchase Points: 548MM§MMM§M—————————————MM§MMonthly Cardholder Report (by Current Balance)MM§M—————————————MM§MBlue Diamond CardholderMM§MAcctNo/Name: 10004 Jenkins, JordanMM§MPrevious Balance: $1,400.00</td>

  </tr>

  <tr>

   <td width="639">MM§MPayment: ($1,400.00)MM§MInterest: $0.00MM§MNew Purchases: $9,000.00MM§MCurrent Balance: $9,000.00MM§MMinimum Payment: $270.00MM§MPurchase Points: 47,500MM§M(includes 10.0% discount rate applied to New Purchases)MM§M(includes 2,500 bonus points added to Purchase Points)MM§MMM§MBlue Diamond CardholderMM§MAcctNo/Name: 10003 King, KellyMM§MPrevious Balance: $1,300.00MM§MPayment: ($150.00)MM§MInterest: $11.50MM§MNew Purchases: $538.20MM§MCurrent Balance: $1,699.70MM§MMinimum Payment: $50.99MM§MPurchase Points: 2,690MM§M(includes 10.0% discount rate applied to New Purchases)MM§MMM§MDiamond CardholderMM§MAcctNo/Name: 10002 Jones, PatMM§MPrevious Balance: $1,200.00MM§MPayment: ($100.00)MM§MInterest: $11.00MM§MNew Purchases: $473.10MM§MCurrent Balance: $1,584.10MM§MMinimum Payment: $47.52MM§MPurchase Points: 1,419MM§M(includes 5.0% discount rate applied to New Purchases)MM§MMM§MSapphire CardholderMM§MAcctNo/Name: 10001 Smith, SamMM§MPrevious Balance: $1,100.00MM§MPayment: ($200.00)MM§MInterest: $9.00MM§MNew Purchases: $548.00MM§MCurrent Balance: $1,457.00MM§MMinimum Payment: $43.71MM§MPurchase Points: 548 MM§MMM§M———————–MM§MInvalid Records ReportMM§M———————–MM§M1;10005;Smith, Pam;110p.0;200.0;34.5;100.0;63.50;350.0 *** invalid numeric value ***MM§M MM§M4;00000;Williams,Pat;1000.0;0.0;34.5;100.0;63.50;300.0 *** invalid category ***MM§M MM§M3;10008;Jenkins, Jordan;1400.0;1400.0;5000.0;1000.0+;4000.0 *** invalid numeric value ***MM§M MM§M2;10006;Jones, Mat;1200.0;1-0.0;34.5;100.0;63.50;300.0 *** invalid numeric value ***MM§M MM§M3;10007;King, Kilby;1300.0;150.0;34.5;$100.0;63.50;300.0;100.0 *** invalid numeric value ***MM§MMM§MMM©M —-jGRASP: operation complete.  </td>

  </tr>

 </tbody>

</table>










<h1><strong>Notes </strong></h1>

<ol>

 <li>This project assumes that you are reading each double value as a String using next() and then parsing it into a double with Double.parseDouble(…) as shown in the following example.     . . . Double.parseDouble(myInput.next());</li>

</ol>

This form of input will throw a <u>java.lang.NumberFormatException</u> if the value is not a double.




If you are reading in each double value as a double using nextDouble(), for example

. . . myInput.nextDouble(); then a <u>java.util.InputMismatchException</u> will be thrown if the value read in is not a double.




For this assignment, you should change your input to use Double.parseDouble(…) rather than nextDouble(), since Web-CAT is looking for <u>NumberFormatException</u> rather than  <u>java.util.InputMismatchException</u>.




<ol start="2">

 <li>If you are using the JUnit Assert.assertArrayEquals method to check two Cardholder arrays for equality, then the equals and hashCode methods must be implemented in your Cardholder class; that is, Assert.assertArrayEquals calls equals(Object obj) on each object in the array, so Cardholder must have an equals method that overrides the one inherited from the Object class. If Cardholder does not override equals(Object obj), then the JUnit Assert.assertArrayEquals method will use the inherited equals(Object obj) method which means two Cardholder arrays will be equal only if they are aliases.</li>

</ol>




Below is a simplified equals method and hashCode method you are free to use.




public boolean equals(Object obj) {          if (!(obj instanceof Cardholder)) {          return false;

}       else {

Cardholder c = (Cardholder) obj;                 return (name.equalsIgnoreCase(c.getName()));

}

}

public int hashCode() {       return 0;

}


