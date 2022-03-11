# Lab Report 5
In this lab report, we will be looking at the difference of my own implementation and lab 9 implementation of `MarkDownParse.java`

We will be looking at two of the test files specficially.

## Find the Difference of Test Result
First of all, we will be finding the difference of two implemetaion by looking at the result of 652 commonmark-spec tests test files provided.

- Open Terminal, login to `ieng6` account
- Find the `result.txt` file of each implementation that we saved during lab 9 (`bash script.sh > result.txt` if you have not done it)
- Use `diff` command accordingly to see the difference between two implementation:

  `diff markdown-parse-BZ/result.txt markdown-parse/result.txt` for my cases
  
  Then you will see a list of difference on test files result of two implementation:
  
![WeChat Screenshot_20220311050808](https://user-images.githubusercontent.com/97600878/157872321-404c019e-84d2-4a29-8e70-2295417fdb1c.png)

One way to visual the difference easier, you can use

`diff -y -W 100  markdown-parse-BZ/result.txt markdown-parse/result.txt`

This allows you to visualize the test case result of each implementation side by side.( `-y` represents side by side and `-W` represents the width):

![WeChat Screenshot_20220311023005](https://user-images.githubusercontent.com/97600878/157872814-47763103-f061-4648-90af-1d0c7aaf92fc.png)

We will be selecting two of the tests to discuss the reason of their different result.
In this case:
- In `test-file/567`, Lab 9 implementation prints out empty bracket`[]`, where My Implementation prints out `[not a link]` which is not suppose to printed.

From visual studio preview, we can tell that the only valid link shoule be `/url1`, so both implementation is incorrect.
![WeChat Screenshot_20220311052243](https://user-images.githubusercontent.com/97600878/157875077-5301ef80-32ee-497b-bc93-c23bbe9153c8.png)


- In `test-file/573`, Lab 9 implementation prints out `[/url]`, where My Implementation prints out empty bracket `[]`.

From visual studio preview, we can tell that there is no valid link, so nothing should be printed. Lab 9 implementation is incorrect.

![WeChat Screenshot_20220311052613](https://user-images.githubusercontent.com/97600878/157876795-ee7e7c99-0caf-4b70-a5a2-c96606bac778.png)

## Fixing
### For test-file 567

Since Both implementation is incorrect, I will be focus on my implementation:

The symptom of the bug is printed out `[not a link]` which are not suppose to print and it does not print out the valid link `[/url]`

Let's look at my implementation first:

![WeChat Screenshot_20220311055617](https://user-images.githubusercontent.com/97600878/157881384-4d08f783-84b7-4b9c-9d5e-95727a4b1e21.png)

For the first part of **printing the invalid link** , as we can see, my implementation does not check if there is any space in between the parentheses, which lead to priting the invalid link.
- Fix:
One way to fix it is that we can add a `spaceIndicator = '  ';`  in the instance variables. Then inside the while loop, we use indexOf to find the index of the space after the open parentheses.
If the index of space apear inbetween the open and close parentheses, we ignore the content inside the parentheses, treated as a invalid link.

For the second part of **not printing the valid link**, my implementation does not check for colon in the md files, which result in ignore of the link.
- Fix:
One way to fix it is that we can add a `colonIndicator = ':';`  in the instance variables. Then inside the while loop, we use indexOf to find the index of the colon.
If after the close bracket and open parentheses, we find the colon, and there is no space in the link, then we treat the link after the colon as a valid link. 
In this case, we also need an `if` statement that search the whole md file, which if there is any bracket with the same content as the one before the colon, we
to assign the same link after the colon to them.(In this test file, in every apearance of `[foo]` reprensents `/url1` ) 

### For test-file 573
For this test file, the lab 9 implementation is incorrect.

The symptom of the bug is it printed `/url`, which is inside the image name that is not suppose to print out

Let's Look at the lab 9 implementation:

![WeChat Screenshot_20220311065739](https://user-images.githubusercontent.com/97600878/157892032-55464f13-5d96-46a3-8918-92684b866ae0.png)

As we can see, this implementation does not have a checker for image to determine whether it is an image or a link.
or a link.

- Fix:
One way to fix it is where in my implementation, I have a `imageIndicator = "!";` to determine if it is an image. If there is a `!` before the open bracket, we find the next close braket with open parentheses, and treat the content inside the bracket as image file name. We can use the similar process in lab 9 implementation to avoiding printing image as a link which is invalid. 

- Additional to that, we can also also consider the case when image turn into hyperlink. In this case, we need to implement conditional statement using the index of each symbol that if there is an image inside bracket that follows by a valid link inside a parentheses, we will treat the link as a valid link as well.

#### This will be all the content for my Lab Report 5. Thanks for watching.


