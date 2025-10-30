
![Zeek cli kung-fu task image.](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/364aa0f61373366b6739d93112688b56.png)  

**CLI Kung-Fu Recall: Processing Zeek Logs**  

Graphical User Interfaces (GUI) are handy and good for accomplishing tasks and processing information quickly. There are multiple advantages of GUIs, especially when processing the information visually. However, when processing massive amounts of data, GUIs are not stable and as effective as the CLI (Command Line Interface) tools.

  

The critical point is: What if there is no "function/button/feature" for what you want to find/view/extract?

  

Having the power to manipulate the data at the command line is a crucial skill for analysts. Not only in this room but each time you deal with packets, you will need to use command-line tools, Berkeley Packet Filters (BPF) and regular expressions to find/view/extract the data you are looking for. This task provides quick cheat-sheet like information to help you write CLI queries for your event of interest.

  


| Category                | Command Purpose and Usage                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Category      | Command Purpose and Usage                                                                                                                                                                                                                                                                                                                       |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Basics                  | View the command history:  <br>`ubuntu@ubuntu$ history`  <br><br>Execute the 10th command in history:  <br>`ubuntu@ubuntu$ !10`<br><br>Execute the previous command:  <br>`ubuntu@ubuntu$ !!`                                                                                                                                                                                                                                                                                                                                                                                                                                   | Read **File** | Read sample.txt file:  <br>`ubuntu@ubuntu$ cat sample.txt`<br><br>Read the first 10 lines of the file:  <br>`ubuntu@ubuntu$ head sample.txt`  <br><br>Read the last 10 lines of the file:  <br>`ubuntu@ubuntu$ tail sample.txt`                                                                                                                 |
| Find  <br>&  <br>Filter | Cut the 1st field:  <br>`ubuntu@ubuntu$ cat test.txt \| cut -f 1`  <br><br>Cut the 1st column:  <br>`ubuntu@ubuntu$ cat test.txt \| cut -c1`  <br><br>Filter specific keywords:  <br>`ubuntu@ubuntu$ cat test.txt \| grep 'keywords'`  <br><br>Sort outputs alphabetically:  <br>`ubuntu@ubuntu$ cat test.txt \| sort`<br><br>Sort outputs numerically:  <br>`ubuntu@ubuntu$ cat test.txt \| sort -n`<br><br>Eliminate duplicate lines:  <br>`ubuntu@ubuntu$ cat test.txt \| uniq`  <br><br>Count line numbers:  <br>`ubuntu@ubuntu$ cat test.txt \| wc -l`  <br><br>Show line numbers  <br>`ubuntu@ubuntu$ cat test.txt \| nl` | Advanced      | Print line 11:  <br>`ubuntu@ubuntu$ cat test.txt \| sed -n '11p'`  <br><br>Print lines between 10-15:  <br>`ubuntu@ubuntu$ cat test.txt \| sed -n '10,15p'`<br><br>Print lines below 11:  <br>`ubuntu@ubuntu$ cat test.txt \| awk 'NR < 11 {print $0}'`  <br><br>Print line 11:  <br>`ubuntu@ubuntu$ cat test.txt \| awk 'NR == 11 {print $0}'` |

|   |   |
|---|---|
|**Special**|Filter specific fields of Zeek logs:<br><br>`ubuntu@ubuntu$ cat signatures.log \| zeek-cut uid src_addr dst_addr`|

|                                                  |                                                                                                  |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| **Use Case**                                     | **Description**                                                                                  |
| `sort \| uniq`                                   | Remove duplicate values.                                                                         |
| `sort \| uniq -c`                                | Remove duplicates and count the number of occurrences for each value.                            |
| `sort -nr`                                       | Sort values numerically and recursively.                                                         |
| `rev`                                            | Reverse string characters.                                                                       |
| `cut -f 1`                                       | Cut field 1.                                                                                     |
| `cut -d '.' -f 1-2`                              | Split the string on every dot and print keep the first two fields.                               |
| `grep -v 'test'`                                 | Display lines that  don't match the "test" string.                                               |
| `grep -v -e 'test1' -e 'test2'`                  | Display lines that don't match one or both "test1" and "test2" strings.                          |
| `file`                                           | View file information.                                                                           |
| `grep -rin Testvalue1 * \| column -t \| less -S` | Search the "Testvalue1" string everywhere, organise column spaces and view the output with less. |