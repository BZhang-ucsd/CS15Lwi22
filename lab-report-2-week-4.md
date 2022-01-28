# Lab Report 2
## Incremental Programming and Debugging


## First Code

### Code change:
![WeChat Screenshot_20220128033738](https://user-images.githubusercontent.com/97600878/151540505-bb494a50-5062-444a-89c0-aa2645a439b0.png)

- Link to the test file: https://github.com/BZhang-ucsd/markdown-parse/blob/main/own-test.md

### Symptom: 

In this case, when we run the test file, we will have a symptom looks like this:
![WeChat Screenshot_20220128062426](https://user-images.githubusercontent.com/97600878/151563990-b83899c6-3af6-4158-b94f-aa62cd30fa12.png)

If we add a checkpoint `System.out.println(currentIndex)` we will find out it creates a infinite loop.
![WeChat Screenshot_20220128062601](https://user-images.githubusercontent.com/97600878/151563999-b5cc821d-0e75-47a5-83f7-d75bfef83a82.png)

The bug in this case is because that in the test file we don't have open bracket, so the `indexOf` will return `-1`, which will then cause the
`closeParen` to have a false value, then leads to the wrong value of `currentIndex`. 

As a result, the `while(currentIndex < markdown.length())`loop will not break after reading the first link, resulting in infinite loop. 

### Fix:
One way to fixed is to add a conditional line which breaks even if there is no Open Bracket.

```
if(nextOpenBracket == -1){
                return toReturn;              
            }
  ```
 
### Result: 
![WeChat Screenshot_20220128073622](https://user-images.githubusercontent.com/97600878/151575735-e3008191-85ba-4022-92bd-017a0302c49d.png)

Now we have the link printed correctly.

## Second Code:

### Code change:
![WeChat Screenshot_20220128033833](https://user-images.githubusercontent.com/97600878/151540627-920e0eb0-c972-4701-a9c8-dc2ac4419ab8.png)

- Link to the test file: https://github.com/aajc/markdown-parse/blob/main/new.md

### Symptom: 

In this case, when we run the test file, we will have a symptom looks like this:

![WeChat Screenshot_20220128072238](https://user-images.githubusercontent.com/97600878/151573386-90a60540-1571-47c6-b423-d137ebeee01b.png)

Here we got the currentIndex from both links, but only one of the link is printed out.

The problem causing the bug is that in the test file we have a line `[google]()(https://google.com)`, where we have a extra parenthesis before the link,
so when the program reads the close paremthesis in `[google]()`, skipping the actual link `(https://google.com)` and find the next open bracket after that. 

### Fix:
One way to fixed the bug is to add a conditional statement, so when there is no content in the first parenthesis, we will looking forward to the next one:

```
if (openParen == closeParen - 1) {
                openParen = markdown.indexOf("(", closeParen + 1);
                closeParen = markdown.indexOf(")", closeParen + 1);
            }
```

### Result: 
![WeChat Screenshot_20220128073509](https://user-images.githubusercontent.com/97600878/151575528-eaf90447-7fbf-4ea0-885b-5a9d56845d27.png)

Now we have both link printed correctly.

## Third Code:

### Code change:
![WeChat Screenshot_20220128034049](https://user-images.githubusercontent.com/97600878/151541020-bd18266e-77ad-4c6b-9e69-772bf97bdead.png)

- Link to the test file: https://github.com/aradomirovicUCSD/markdown-parse/blob/main/new-new-file.md

### Symptom: 

In this case, when we run the test file, we will have a symptom looks like this:
![WeChat Screenshot_20220128074511](https://user-images.githubusercontent.com/97600878/151581062-8a64cd19-5299-4572-a572-4782b45f9efa.png)


Where it prints the name of the image as it is a link.

The problem is caused because the link of an image file also has open bracket, the program can not determine if it is a link to an image file or a link, so it will treated it as a link, scan and printed. 

### Fix:
One way to fixed is that, we know the syntax of image file will have a exclamation mark, so we can initial an integer variable called `nextExclation` for the index of Exclamation mark, and add a conditional statement for the program to distinguish between link and image:

```
int nextExclamation = markdown.indexOf("!", currentIndex);
if((nextExclamation != nextOpenBracket - 1 || nextExclamation < 0) && openParen == nextCloseBracket + 1) toReturn.add(markdown.substring(openParen + 1, closeParen));
```

### Result: 

![WeChat Screenshot_20220128080440](https://user-images.githubusercontent.com/97600878/151580692-a5caf49f-ed6c-4e65-b838-ffe6ca1455a3.png)

Now we have only the two links printed, not the name of the image.

## End of Lab Report



