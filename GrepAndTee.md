# Grep
-1The grep command in Linux is a powerful text-search utility used to find patterns (text or regular expressions) within files or input streams. Its name stands for "Global Regular Expression Print".

**Basic Syntax:**
```bash
grep [options] "pattern" [file(s)]
```
Common Uses of grep:
Search for a string in a file:

```bash
grep "error" logfile.txt
```
(Finds all lines containing "error" in logfile.txt)

Case-insensitive search (-i):

```bash
grep -i "warning" system.log
(Matches "Warning", "WARNING", etc.)
```
Search recursively in directories (-r or -R):

```bash
grep -r "main()" /home/user/projects/
(Searches for "main()" in all files under /home/user/projects/)
```
Invert match (find lines NOT containing the pattern) (-v):

```bash
grep -v "success" results.txt
(Shows lines that do not contain "success")
```
Count matching lines (-c):

```bash
grep -c "404" access.log
(Returns the number of lines with "404" in access.log)
```
Show line numbers (-n):

```bash
grep -n "fatal" error.log
(Displays line numbers along with matches)
```
Search for whole words only (-w):

```bash
grep -w "port" config.txt
(Matches "port" but not "export" or "portal")
```
Use extended regular expressions (-E):

```bash
grep -E "error|fail" system.log
(Searches for either "error" or "fail")
```
Pipe output from another command into grep:

```bash
ps aux | grep "nginx"
(Finds all running processes containing "nginx")
```
Search in compressed files (zgrep):

```bash
zgrep "exception" /var/log/syslog.1.gz
(Searches inside a compressed log file)
```
**Why is grep useful?**
- Quickly find errors in log files.
- Filter command outputs (e.g., ls, ps, netstat).
- Search codebases for functions/variables.
  Automate text processing in scripts.
- Variants of grep:
- egrep = grep -E (extended regex)
- fgrep = grep -F (fixed strings, no regex)
- rgrep = recursive grep
- zgrep = search in compressed files

**grep also used to store the output from another command?**

- The grep command itself does not store output—it only filters text. However, you can combine grep with other commands to save its output to a file. Here’s how:

**1. Store grep Output to a File (Using Redirection >)**
- If you want to save the filtered results from grep into a file, use the > (overwrite) or >> (append) redirection operators.

Example: Search & Save to a File
```bash
grep "error" /var/log/syslog > errors.txt
```
- This extracts all lines containing "error" from /var/log/syslog and saves them in errors.txt (overwriting if the file exists).

**Append Instead of Overwrite (>>)**
```bash
grep "warning" /var/log/syslog >> logs_combined.txt
```
- Adds matching lines to the end of logs_combined.txt (keeps old content).

**2. Combine grep with tee to View & Save Simultaneously**
- If you want to see the output on screen AND save it to a file, use tee:
```bash
grep -r "TODO" ~/projects/ | tee todo_list.txt
```
Recursively searches for "TODO" in ~/projects/, displays results in the terminal, and saves them to todo_list.txt.

**Key Notes:**
- grep only filters—it doesn’t store by itself.
- Use > to overwrite a file or >> to append.
- Combine with pipes (|) to filter another command’s output before saving.
- Use tee for real-time viewing + saving.

## > &&  >> it just store the output and it will not display in the terminal?
## Yes! When you use > (overwrite) or >> (append) to redirect output to a file, the result is only saved to the file and not displayed in the terminal.

**Key Differences:**
Command	Effect
- grep "foo" file	Output is displayed in the terminal (not saved).
- grep "foo" file > output.txt	Output is saved to output.txt (terminal shows nothing).
- grep "foo" file >> output.txt	Output is appended to output.txt (terminal shows nothing).
- grep "foo" file | tee output.txt	Output is displayed and saved to output.txt.
- grep "foo" file | tee -a output.txt	Output is displayed and appended to output.txt.
Examples:
**1. Silent Save (No Terminal Output)**
```bash
grep "error" /var/log/syslog > errors.log  # Overwrites file, no terminal output
grep "warning" /var/log/syslog >> logs.txt # Appends, no terminal output
```
**2. Display & Save (Using tee)**
```bash
grep "404" access.log | tee 404_errors.log      # Shows results AND saves
grep "GET" access.log | tee -a all_requests.log # Shows AND appends
```
**3. Store Command Output (e.g., ls, ps)**
```bash
ls -l | grep ".txt" > text_files.txt  # Saves names of all .txt files
ps aux | grep "nginx" > nginx_procs.txt # Saves Nginx processes
```
## When to Use Which?
### > or >> → When you only want to save output (no terminal display). tee → When you want to see output AND save it. ###
