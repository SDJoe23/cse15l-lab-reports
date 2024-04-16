# Lab Report 5

## Part 1 Debugging a Java Application: A Comprehensive Guide
Introduction

In this blog post, we'll walk through a common issue faced by Java developers: handling InputMismatchException when processing mixed content in text files. Through a simulated scenario on an educational forum, we'll explore a student's problem, a teaching assistant's (TA) guidance, and the student's resolution of the issue involving a Java application, DataAnalyzer.java, designed to read integers from a file and calculate their sum.

## Original Student Post on EdStem

Title: Runtime Exception When Summing Integers from File in Java

Content:

Hello everyone,

I've encountered a runtime exception while trying to sum integers from a file using my Java program. The program is supposed to read integers from data.txt and calculate their sum, but it crashes with an InputMismatchException when I run it with certain files. Here's the code:

My Java application attempts to read integers from a file and calculate their sum.

```bash
import java.io.File;
import java.util.Scanner;

public class DataAnalyzer {
    public static void main(String[] args) {
        try {
            File file = new File("data.txt");
            Scanner scanner = new Scanner(file);
            int sum = 0;
            while (scanner.hasNext()) {
                int data = scanner.nextInt(); // This line can throw an InputMismatchException
                sum += data;
            }
            scanner.close();
            System.out.println("Sum of the integers: " + sum);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Bash Script (runAnalysis.sh)
This script compiles and runs the Java application. It assumes the presence of DataAnalyzer.java and data.txt in the same directory.

```bash
#!/bin/bash
# Compiles the DataAnalyzer Java program
javac DataAnalyzer.java

# Runs the compiled Java program
java DataAnalyzer
To give execute permission to the script:
```

And here's the error message I get:

```bash
Exception in thread "main" java.util.InputMismatchException
    at java.util.Scanner.throwFor(Scanner.java:864)
    at java.util.Scanner.next(Scanner.java:1485)
    at java.util.Scanner.nextInt(Scanner.java:2117)
    at DataAnalyzer.main(DataAnalyzer.java:10)
```

I suspect the issue might be due to non-integer values in data.txt, but I'm not sure how to confirm or fix this. Any advice would be greatly appreciated! Here is my code.

Student's Java Application (DataAnalyzer.java)


Thank you!

## TA Response

Hello,

It looks like you're on the right track suspecting that non-integer values in data.txt are causing the InputMismatchException. This exception occurs when the Scanner.nextInt() method encounters a token that it cannot parse as an integer. I can see that the problems is coming from this part of the code:

```bash
while (scanner.hasNext()) {
    int data = scanner.nextInt(); // This line can throw an InputMismatchException
    sum += data;
}
```

To confirm this, you could inspect data.txt for non-integer values. Additionally, you could modify your code to catch this exception specifically and print a helpful message, or even better, check if the next token is an integer using scanner.hasNextInt() before trying to read it as an integer. Could you try adding a check for scanner.hasNextInt() in your loop and see if that resolves the issue? Try this:

```bash
chmod +x runAnalysis.sh
```

Then, run the script with:

```bash
./runAnalysis.sh
```

Best regards,
TA

## Student Follow-Up
Hi TA,

Thanks for your suggestion! I modified my loop to include a check for scanner.hasNextInt(), and it worked! Here's the updated loop:

```bash
while (scanner.hasNext()) {
    if (scanner.hasNextInt()) {
        int data = scanner.nextInt();
        sum += data;
    } else {
        System.out.println("Skipping non-integer value: " + scanner.next());
    }
}
```

After making this change, my program now skips over non-integer values and sums only the integers in data.txt. No more InputMismatchException!This is a great learning moment for me on handling input validation. Thank you for the help!

## Debugging Scenario Setup and Solution Summary
Debugging InputMismatchException in DataAnalyzer.java
Setup and Problem Description:
Directory Structure:
DataAnalyzerProject/
DataAnalyzer.java
data.txt
runAnalysis.sh

Contents Before Fix:

DataAnalyzer.java:

```bash
import java.io.File;
import java.util.Scanner;

public class DataAnalyzer {
    public static void main(String[] args) {
        try {
            File file = new File("data.txt");
            Scanner scanner = new Scanner(file);
            int sum = 0;
            while (scanner.hasNext()) {
                int data = scanner.nextInt(); // This line can throw an InputMismatchException
                sum += data;
            }
            scanner.close();
            System.out.println("Sum of the integers: " + sum);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

data.txt: (Contents causing the issue)

```bash
10
20
Hello
30
```

runAnalysis.sh:

```bash
#!/bin/bash
# Compiles the DataAnalyzer Java program
javac DataAnalyzer.java

# Runs the compiled Java program
java DataAnalyzer
```

Commands to Trigger the Bug:

Ensure runAnalysis.sh is executable:

```bash
chmod +x runAnalysis.sh
```
Run the script:

```bash
./runAnalysis.sh
```
Triggered Bug:

Running these commands with the provided data.txt content causes an InputMismatchException because of the non-integer value ("Hello") present in the file, which the Scanner.nextInt() method cannot parse.

Solution to Fix the Bug:

Edit DataAnalyzer.java to include a check for integer values before attempting to read them. This involves modifying the while loop as follows:

Modified Loop in DataAnalyzer.java:

```bash
while (scanner.hasNext()) {
    if (scanner.hasNextInt()) {
        int data = scanner.nextInt();
        sum += data;
    } else {
        // Skip over non-integer values and print a message
        System.out.println("Skipping non-integer value: " + scanner.next());
    }
}
```

This modification allows the program to skip over any non-integer values encountered in data.txt, thereby avoiding the InputMismatchException and summing only the integer values.

## Conclusion
This blog post provided a detailed walkthrough of identifying and solving a common issue related to data type mismatches during file processing in Java. Through iterative debugging, guided by TA advice, the student learned a valuable lesson in programming best practices and input validation, showcasing the educational value of collaborative problem-solving in coding communities.

## Part 2 What Have I Learned
In the second half of this quarter, my lab experience significantly deepened my appreciation and understanding of vim, beyond the basics of opening and editing files. The intensive use of vim's modal editing—switching between insert, command, and visual modes—revolutionized my text editing efficiency, eliminating reliance on the mouse. I was particularly enlightened by vim's powerful features such as search and replace, and the ability to use buffers, windows, and tabs for multitasking. This transformed vim from a simple editor to an advanced tool tailored to my needs, dramatically enhancing my coding workflow and collaborative abilities. This deeper engagement with vim has not only made me a more proficient coder but has also enriched my problem-solving skills.
