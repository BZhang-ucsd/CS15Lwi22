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
From VScode preview, this should produce: `[url.com,google.com,google.com]`

![snippet1](https://user-images.githubusercontent.com/97600878/155805105-3550996a-95af-40ca-adac-05eb624b3a0c.png)

### Testing
```
@Test
    public void Snippet1Test() throws IOException {
        String file=Files.readString(Path.of("Snippet1.md"));
        assertEquals(List.of("url.com, google.com, google.com"),MarkdownParse.getLinks(file));
    }
```
#### Own implementation
we can see the test failed because there is one extra backtick in the printed links.

![WeChat Screenshot_20220225134801](https://user-images.githubusercontent.com/97600878/155807663-8a5b0418-5d27-48d5-b7a6-bcde5494c480.png)

#### Review Implementation
In the Review Implemetation, Same result occurs.

![WeChat Screenshot_20220225134856](https://user-images.githubusercontent.com/97600878/155807781-84a4d57d-0c17-43be-b614-7b15e67b4b5c.png)

### Snippet 2
```
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)
```
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

