# Lab Report 4

## We will be looking at two different implementation of markdown-parse in this report.

Here is the link for my own markdown-parse repository: https://github.com/BZhang-ucsd/markdown-parse

Here is the link for the markdown-parse repository that I reviewd: https://github.com/nseyoum/CSE15L-Platypus

We will be testing on these three markdown snippet:

## Snippet 1
```
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```
From VScode preview, this should produce: `` [`google.com,google.com,ucsd.edu] ``

![WeChat Screenshot_20220225143015](https://user-images.githubusercontent.com/97600878/155811849-a3cfdaf4-1826-45c5-9d0e-1d69c3c45e84.png)

### Testing
```
@Test
    public void Snippet1Test() throws IOException {
        ArrayList<String> str = new ArrayList<String>();
        str.add("`google.com");
        str.add("google.com");
        str.add("ucsd.edu");
        String file=Files.readString(Path.of("Snippet1.md"));
        assertEquals(str,MarkdownParse.getLinks(file));
    }
```
#### Own implementation
we can see the test failed

![WeChat Screenshot_20220225134801](https://user-images.githubusercontent.com/97600878/155807663-8a5b0418-5d27-48d5-b7a6-bcde5494c480.png)

#### Review Implementation
In the Review Implemetation, Same result occurs.

![WeChat Screenshot_20220225134856](https://user-images.githubusercontent.com/97600878/155807781-84a4d57d-0c17-43be-b614-7b15e67b4b5c.png)

#### Fix
To make the program works for snippet1, we can add an if statement in the MarkdownParse.java, so if there is backtip infront of the open bracket, we will skip it to the
next appropriate link
```
int nextBacktick = markdown.indexOf("`", currentIndex);
if(nextBacktick == 0){
                currentIndex = closeParen + 1;
            }
```
For `[`code]`](ucsd.edu)` we can modify the line that we find the close bracket to ignore the extra close braket and backtick.
`
int nextCloseBracket = markdown.indexOf("](", nextOpenBracket);
`
If we run the single test on snippet 1 again:

![WeChat Screenshot_20220225142046](https://user-images.githubusercontent.com/97600878/155811029-e4e04c38-27fb-4ec1-9690-90c736ab4ed6.png)

### Snippet 2
```
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)
```

From VScode preview, this should produce: `[a.com,a.com(()),example.com]`

![WeChat Screenshot_20220225143150](https://user-images.githubusercontent.com/97600878/155811978-1ac19581-3f9e-47d9-94b8-4c9b0cb44a0d.png)

### Testing
```
@Test
    public void Snippet2Test() throws IOException {
        ArrayList<String> str = new ArrayList<String>();
        str.add("a.com");
        str.add("a.com(())");
        str.add("example.com");
        String file=Files.readString(Path.of("Snippet2.md"));
        assertEquals(str,MarkdownParse.getLinks(file));
    }
```
#### Own implementation
we can see the test failed

![WeChat Screenshot_20220225153236](https://user-images.githubusercontent.com/97600878/155816893-0a09b7ab-f9ed-418a-9605-562ddfe60b7e.png)


#### Review Implementation
In the Review Implemetation:

![WeChat Screenshot_20220225155736](https://user-images.githubusercontent.com/97600878/155818841-4c45d489-1e4e-4f26-9eb7-5183322013c7.png)

#### Fix
I think it is difficult to fix in a small change. This error might be solve if we can count the number of open parentheses and skip the same amount of close parenthese 
in the link before we reach the close parenthese of the entire link.

### Snippet 3
```
[this title text is really long and takes up more than 
one line

and has some line breaks](
    https://www.twitter.com
)

[this title text is really long and takes up more than 
one line](
    https://ucsd-cse15l-w22.github.io/
)


[this link doesn't have a closing parenthesis](github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



)

And then there's more text
```

From VScode preview, this should produce: `[https://www.twitter.com,https://ucsd-cse15l-w22.github.io/, https://cse.ucsd.edu/]`

![WeChat Screenshot_20220225143217](https://user-images.githubusercontent.com/97600878/155812156-2fcdde3f-658f-481e-9090-dc6b8ef273ad.png)

### Testing
```
@Test
    public void Snippet3Test() throws IOException {
        ArrayList<String> str = new ArrayList<String>();
        str.add("https://www.twitter.com");
        str.add("https://ucsd-cse15l-w22.github.io/");
        str.add("https://cse.ucsd.edu/");
        String file=Files.readString(Path.of("Snippet3.md"));
        assertEquals(str,MarkdownParse.getLinks(file));
    }
```
#### Own implementation
we can see the test failed:

![WeChat Screenshot_20220225155822](https://user-images.githubusercontent.com/97600878/155818895-652e5e7a-7820-4606-837c-010940c35d87.png)

#### Review Implementation
In the Review Implemetation:

![WeChat Screenshot_20220225160337](https://user-images.githubusercontent.com/97600878/155819174-952fe2b9-9a87-42ec-be57-d59377a283b6.png)

#### Fix
To fix this issue, we can create a if statement which if Next Open Braket comes before the close parentheses, we update the currentIndex and skip the broken link without
close parentheses.
