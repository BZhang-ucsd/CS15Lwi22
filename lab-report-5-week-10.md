# Lab Report 6
In this lab report, we will be looking at the difference of my own implementation and lab 9 implementation of `MarkDownParse.java`

We will be looking at two of the test cases specficially.

## Find the Difference of Test Result
First of all, we will be finding the difference of two implemetaion by looking at the result of 652 commonmark-spec tests test cases provided.

- Open Terminal, login to `ieng6` account
- Find the `result.txt` file of each implementation that we saved during lab 9 (`bash script.sh > result.txt` if you have not done it)
- Use `diff` command accordingly to see the difference between two implementation:

  `diff markdown-parse-BZ/result.txt markdown-parse/result.txt` for my cases
  
  Then you will see a list of difference on test cases result of two implementation:
  
![WeChat Screenshot_20220311050808](https://user-images.githubusercontent.com/97600878/157872321-404c019e-84d2-4a29-8e70-2295417fdb1c.png)

One way to visual the difference easier, you can use

`diff -y -W 100  markdown-parse-BZ/result.txt markdown-parse/result.txt`

This allows you to visualize the test case result of each implementation side by side.( `-y` represents side by side and `-W` represents the width):

![WeChat Screenshot_20220311023005](https://user-images.githubusercontent.com/97600878/157872814-47763103-f061-4648-90af-1d0c7aaf92fc.png)

We will be selecting two of the tests to discuss the reason of their different result.
In this case:
- In `test-case/567`, Lab 9 implementation prints out empty bracket`[]`, where My Implementation prints out `[not a link]` which is not suppose to printed.

From visual studio preview, we can tell that the only valid link shoule be `/url1`, so both implementation is incorrect.
![WeChat Screenshot_20220311052243](https://user-images.githubusercontent.com/97600878/157875077-5301ef80-32ee-497b-bc93-c23bbe9153c8.png)


- In `test-case/573`, Lab 9 implementation prints out `[/url]`, where My Implementation prints out empty bracket `[]`.

From visual studio preview, we can tell that there is no valid link, so nothing should be printed. Lab 9 implementation is incorrect.

![WeChat Screenshot_20220311052613](https://user-images.githubusercontent.com/97600878/157876795-ee7e7c99-0caf-4b70-a5a2-c96606bac778.png)

## Fixing
- For test case 567
Since Both implementation is incorrect, I will be focus on my implementation:
The symptom of the bug is printed out `[not a link]` which are not suppose to print and it does not print out the valid link `[/url]`



