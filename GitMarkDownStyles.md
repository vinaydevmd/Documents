__This file helps you to edit MarkDown (*.md) file__

https://guides.github.com/features/mastering-markdown/

__Syntax guide__
Here’s an overview of Markdown syntax that you can use anywhere on GitHub.com or in your own text files.

# Headers

# This is an <h1> tag
## This is an <h2> tag
###### This is an <h6> tag

# Emphasis

  *This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

_You **can** combine them_

# Lists
# Unordered
* Item 1
* Item 2
  * Item 2a
  * Item 2b
  
# Odered
1. Item 1
1. Item 2
1. Item 3
   1. Item 3a
   1. Item 3b


# Images
![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)

# Links
http://github.com - automatic!
[GitHub](http://github.com)

#Blockquotes
As Kanye West said:

> We're living the future so
> the present is our past.

# Inline code
I think you should use an
`<addr>` element here instead.

#Syntax Highlighting
[GitHub Flavored Markdown:](https://help.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax)

```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```

You can also simply indent your code by four spaces:



function fancyAlert(arg) {
      if(arg) {
        $.facebox({div:'#foo'})
      }
    }
    
Here’s an example of Python code without syntax highlighting:

def foo():
    if not bar:
        return True
        
        
#Task Lists

- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported 
- [x] list syntax required (any unordered or ordered list supported) 
- [x] this is a complete item 
- [ ] this is an incomplete item


You can indicate emphasis with bold, italic, or strikethrough text.
[Basic Writing and Fromatting syntax](https://help.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax)

