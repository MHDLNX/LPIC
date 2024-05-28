The `sed` command, short for "stream editor," is a powerful utility in Unix and Unix-like operating systems used for parsing and transforming text. It can perform a variety of text manipulations, making it a valuable tool for text processing tasks. Here’s a comprehensive overview of the `sed` command along with examples:

### Basic Usage
The basic syntax for the `sed` command is:
```
sed [options] 'script' [input-file]
```

### Common Options

1. **`-e script`**:
   - Adds the `script` to the commands to be executed.
   
2. **`-f script-file`**:
   - Takes the `script` from the specified file.

3. **`-i[SUFFIX]`**:
   - Edits files in place (modifies the original file). Optionally, a backup of the original file is made if `SUFFIX` is provided.

4. **`-n`**:
   - Suppresses automatic printing of pattern space. Useful when you only want to print specific lines.

### Basic Commands

1. **`s/regexp/replacement/flags`**:
   - Substitutes the first occurrence of `regexp` (regular expression) with `replacement` in each line.
   
2. **`p`**:
   - Prints the current pattern space.
   
3. **`d`**:
   - Deletes the pattern space; immediately starts the next cycle.
   
4. **`q`**:
   - Exits `sed` after processing the first line or the first occurrence of a pattern.

5. **`a\text`**:
   - Appends `text` after each line matching the address.

6. **`i\text`**:
   - Inserts `text` before each line matching the address.

7. **`c\text`**:
   - Changes lines matching the address with `text`.

### Examples

1. **Substitute Text**:
   ```
   echo "Hello World" | sed 's/World/Universe/'
   ```
   Output:
   ```
   Hello Universe
   ```
   This substitutes the first occurrence of "World" with "Universe".

2. **Substitute Text Globally**:
   ```
   echo "foo bar foo" | sed 's/foo/baz/g'
   ```
   Output:
   ```
   baz bar baz
   ```
   The `g` flag substitutes all occurrences of "foo" with "baz".

3. **Delete Lines Containing a Pattern**:
   ```
   sed '/pattern/d' filename
   ```
   This deletes all lines containing "pattern" from the file `filename`.

4. **Print Specific Lines**:
   ```
   sed -n '5,10p' filename
   ```
   This prints lines 5 through 10 from the file `filename`.

5. **In-place Editing with Backup**:
   ```
   sed -i.bak 's/old/new/g' filename
   ```
   This substitutes "old" with "new" in `filename`, and creates a backup file named `filename.bak`.

6. **Append Text After a Line Matching a Pattern**:
   ```
   echo -e "line1\nline2" | sed '/line1/a\This is appended'
   ```
   Output:
   ```
   line1
   This is appended
   line2
   ```
   This appends "This is appended" after lines matching "line1".

7. **Insert Text Before a Line Matching a Pattern**:
   ```
   echo -e "line1\nline2" | sed '/line1/i\This is inserted'
   ```
   Output:
   ```
   This is inserted
   line1
   line2
   ```
   This inserts "This is inserted" before lines matching "line1".

8. **Change Lines Matching a Pattern**:
   ```
   echo -e "line1\nline2" | sed '/line1/c\This is changed'
   ```
   Output:
   ```
   This is changed
   line2
   ```
   This changes lines matching "line1" to "This is changed".

9. **Print Lines Containing a Pattern**:
   ```
   sed -n '/pattern/p' filename
   ```
   This prints only the lines that contain "pattern" from the file `filename`.

10. **Using Multiple Commands**:
    ```
    sed -e 's/old/new/' -e '/pattern/d' filename
    ```
    This substitutes "old" with "new" and deletes lines containing "pattern" from the file `filename`.

### Summary

The `sed` command is an essential tool for text processing in Unix-like systems. It provides powerful capabilities to manipulate and transform text data directly from the command line or within scripts. Understanding its basic and advanced features can significantly enhance your ability to handle text files and automate text-related tasks.

<hr>

## additional note 

- remove the lines which contain comment (#) and also empty lines : `cat index.txt | sed /^#/d | sed /^$/d`
- 
