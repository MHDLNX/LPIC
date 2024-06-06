In the world of Unix and Linux, text processing tools are a fundamental part of the ecosystem, enabling the manipulation of data streams and files in powerful and flexible ways.

Among these tools, AWK stands out as a versatile command-line utility that excels in processing structured text, such as CSVs, logs, and other data files. For DevOps engineers, familiar with AWK command can significantly enhance the ability to automate and streamline tasks related to data parsing, reporting, and system administration.

# **What is AWK**

AWK, named after its creators Aho, Weinberger, and Kernighan, is a scripting language designed for text processing. With its straightforward syntax, AWK is highly effective at searching files for lines that contain certain patterns and performing specified actions on those lines. AWK is not just a command; it’s a complete programming language that offers variables, flow control statements, arrays, and functions.

## **Key Features of AWK**

- **Pattern scanning and processing:** AWK scans a file line by line, searching for patterns specified by the user. When a line matches one of the patterns, AWK executes the associated action.
- **Built-in text processing functions:** It includes a set of functions for string manipulation, arithmetic operations, and input/output, making it a robust tool for text processing.
- **Field-oriented text processing:** AWK treats each line as a record and each space-separated word as a field, simplifying the processing of structured text.

# **Get Started**

Let’s prepare the following sample output from `netstat` command:

```
$ cat netstat.txt
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp        0      0 192.168.1.5:22          192.168.1.1:53822       ESTABLISHED
tcp6       0      0 :::80                   :::*                    LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
udp        0      0 0.0.0.0:68              0.0.0.0:*
udp6       0      0 :::546                  :::*
```

Now let’s call a simple `awk` command:

```
$ awk '{print $1, $4}' netstat_output.txt
Proto Local
tcp 127.0.0.1:3306
tcp 0.0.0.0:22
tcp 192.168.1.5:22
tcp6 :::80
tcp6 :::22
udp 0.0.0.0:68
udp6 :::546
```

Here’s a breakdown of the command:

- `awk`: Invokes the AWK program, which is designed for pattern scanning and processing of text.
- `'{print $1, $4}'`: Specifies an action to be performed on each line of the input file. In AWK, actions are enclosed in curly braces `{}`. This particular action tells AWK to print the first (`$1`) and fourth (`$4`) fields of each line, separated by a space. Fields in AWK are typically whitespace-separated words in a line, though this can be customized.

# **AWK Filter**

AWK programs are structured around the concept of patterns and actions, written as:

```
pattern { action }
```

- Pattern: This can be a regular expression, a relational expression, a range pattern, or even a special pattern (`BEGIN` or `END`). When a line of input matches the pattern, AWK executes the associated action. If no pattern is specified, the action is executed for every line of input.
- Action: This is a block of AWK commands enclosed in curly braces `{ ... }` that is executed when the input matches the pattern. Actions can modify data, compute results, or produce output.

## **How Filtering Works**

- Reading Input: AWK reads input line by line, splitting each line into fields based on a field separator (default is whitespace).
- Applying Patterns: For each line, AWK evaluates the specified patterns in the order they appear in the script. A pattern could be as simple as a condition on field values (`$1 == "somevalue"`) or a regular expression match (`/regex/`).
- Executing Actions: When a line matches a pattern, AWK performs the corresponding action on that line. Actions can include printing or modifying fields, performing calculations, or any other operations AWK supports.
- Continuing the Process: This process repeats for each line of the input until all input is consumed.

For example:

```
$ awk '$3==0 && $6=="LISTEN"' netstat_output.txt
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp6       0      0 :::80                   :::*                    LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
```

In the above command:

- `$3==0`: This condition checks if the third field (`$3`) of each line is equal to `0`.
- `$6=="LISTEN"`: This condition checks if the sixth field (`$6`) is exactly equal to the string "LISTEN".
- `&&`: This is the logical AND operator. It combines the two conditions, meaning that both conditions must be true for the action part of the AWK script to be executed. If either condition is false, the line is not processed further. Other available logical operators are: `!=`, `>`, `<`, `>=`, `<=`.

If we want to include the header, we can make use of the built-in variable NR:

```
$ awk '$3==0 && $6=="LISTEN" || NR==1' netstat_output.txt
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp6       0      0 :::80                   :::*                    LISTEN
tcp6       0      0 :::22                   :::*                    LISTEN
```

Some common AWK predefined variables:

# **AWK String Matching**

AWK processes text by reading one line at a time, dividing each line into fields, and examining each field or the entire line against specified patterns. These patterns can be literal strings, regular expressions, or a combination of both, enabling a flexible approach to finding matches. When a match is found, AWK performs designated actions on the line, such as printing it to the screen, saving it to a file, or even modifying the text on the fly.

## **Literal Strings and Regular Expressions**

AWK supports two main types of string matching: literal strings and regular expressions. Literal string matching is as simple as looking for an exact word or phrase within the text. For example, searching for the word “error” in a log file could be as simple as:

```
$ awk '/error/' example.log
...
2023-07-01 10:05:00 Error: Connection timeout
...
```

Regular expressions offer a more powerful and flexible way to search for patterns. For example, to match any line that starts with a date in the `YYYY-MM-DD` format:

```
$ awk '/^[0-9]{4}-[0-9]{2}-[0-9]{2}/' example.log
```

## **Field-Specific Matching**

One of AWK’s strengths is its ability to perform field-specific searches. By default, AWK considers spaces and tabs as field separators, allowing for targeted searches within specific fields. For instance, if you wanted to find lines where the second field indicates an “Error”:

```
$ awk '$3 == "Error:"' example.log
2023-07-01 10:05:00 Error: Connection timeout
```

# **AWK Splitting Files**

Splitting files with AWK is straightforward, utilizing redirection. The following example demonstrates splitting a file based on the 6th field, which is quite simple (where `NR!=1` indicates that the header is not processed).

Consider a scenario where we want to use AWK to split a CSV file into multiple files based on a specific field’s value. For this example, imagine we have a CSV file named `employees.csv` with the following content:

```
ID,Name,Department,Salary
1,John Doe,Engineering,50000
2,Jane Smith,Marketing,45000
3,Emily Davis,Engineering,55000
4,Chris Brown,Marketing,40000
```

We want to split this file into separate files for each department, excluding the header from the split files. The AWK command we will run is:

```
$ awk -F, 'NR!=1{print > $3".csv"}' employees.csv
```

- `F,`: Sets the field separator to a comma, as we're dealing with a CSV file.
- `NR!=1`: This condition skips the first record (header line).
- `print > $3".csv"`: For each line (excluding the header), this command prints the entire line into a file named after the value in the 3rd field (Department) with a `.csv` extension. Thus, lines belonging to the same department are collected into their respective files.

The above command will create the following two files:

Engineering.csv:

```
1,John Doe,Engineering,50000
3,Emily Davis,Engineering,55000
```

Marketing.csv:

```
2,Jane Smith,Marketing,45000
4,Chris Brown,Marketing,40000
```

# **AWK Statistics**

Let’s take an example where we have a CSV file named `sales_data.csv` containing sales records for different products over various months. Our goal is to use AWK to calculate the total sales for each product and then display the results.

sales_data.csv:

```
Product,Month,Sales
WidgetA,January,150
WidgetB,February,90
WidgetA,March,200
WidgetC,January,400
WidgetB,March,120
WidgetC,February,300
```

Let’s run the following command:

```
$ awk -F, 'NR>1 {sales[$1]+=$3} END {for (product in sales) print product ", Total Sales: " sales[product]}' sales_data.csv
```

The expected output will look like:

```
WidgetA, Total Sales: 350
WidgetB, Total Sales: 210
WidgetC, Total Sales: 700
```

Another example is to count file size. The following command calculates the total size of all C files, CPP files, and H files.

```
$ ls -l  *.cpp *.c *.h | awk '{sum+=$5} END {print sum}'
```

# **AWK Script**

An AWK script is a powerful tool for text processing and data extraction, widely used in Unix-like operating systems. It operates on a series of records and fields, applying specified patterns and actions on the text. AWK scripts can be used for a variety of tasks, such as data summarization, report generation, and text manipulation.

## **Structure of an AWK Script**

An AWK script typically follows this structure:

```
pattern { action }
pattern { action }
...
```

- **Pattern**: A condition or regex that determines which records (usually lines of text) the action should apply to. If a pattern is omitted, the action applies to all records.
- **Action**: A block of AWK commands enclosed in curly braces `{}` that is executed when the pattern matches a record. Actions can include printing or modifying text, performing calculations, and more.

## **Running an AWK Script**

AWK scripts can be run in two ways:

- Inline with the `awk` command: The script is passed as an argument to `awk`.

```
$ awk 'script' input_file
```

- Stored in a file: The script is written into a file and passed to `awk` using the `f` option.

```
$ awk -f script_file.awk input_file
```

Suppose you have a CSV file named `sales.csv` with the following content:

```
Month,Product,Sales
January,Apples,100
February,Apples,150
January,Bananas,90
February,Bananas,95
```

You want to calculate the total sales for each product. The AWK script in a file, say `summarize_sales.awk`, will look like:

```
BEGIN { FS = "," }
NR > 1 { sales[$2] += $3 }
END {
  for (product in sales)
    print product, sales[product]
}
```

# **Conclusion**

In conclusion, AWK stands out as a robust tool for developers, system administrators, and data analysts alike. Its blend of simplicity, efficiency, and power makes it an invaluable asset for anyone looking to perform text processing and data analysis on Unix-like systems.

Whether dealing with large datasets, streamlining log files, or automating report generation, AWK provides the functionality and flexibility needed to efficiently accomplish these tasks, demonstrating its enduring relevance and utility in the field of computing.
