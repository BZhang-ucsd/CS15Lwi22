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
- 

