# Github Flavored Markdown extension syntax 
___
## ***Strikethrough***
#### Any word wrapped with two tildes (like \~\~this\~\~) will appear crossed out.
#### Example :
```
~~Hi!~~ Nice to meet you!
```

#### As with regular emphasis delimiters, a new paragraph will cause strikethrough parsing to cease:
##### Example :
```
Nice to ~~meet
you!~~
```
___
## ***Autolink***
#### GFM enables the autolink extension, where autolinks will be recognised in a greater number of conditions.

#### The scheme http will be inserted automatically:
##### Example :
```
www.naver.com
```
#### After a valid domain, zero or more non-space non-< characters may follow:
##### Example :
```
Visit www.commonmark.org/help for more information.
```
#### We then apply extended autolink path validation as follows:
#### Trailing punctuation (specifically, ?, !, ., ,, :, *, _, and ~) will not be considered part of the autolink, though they may be included in the interior of the link:
```
Visit www.commonmark.org.

Visit www.commonmark.org/a.b.
```
#### When an autolink ends in ), we scan the entire autolink for the total number of parentheses. If there is a greater number of closing parentheses than opening ones, we don’t consider the unmatched trailing parentheses part of the autolink, in order to facilitate including an autolink inside a parenthesis:
##### Example :
```
ww.google.com/search?q=Markup+(business)

www.google.com/search?q=Markup+(business)))

(www.google.com/search?q=Markup+(business))

(www.google.com/search?q=Markup+(business)
```
#### This check is only done when the link ends in a closing parentheses ), so if the only parentheses are in the interior of the autolink, no special rules are applied:
##### Example :
```
www.google.com/search?q=(business))+ok
```
#### If an autolink ends in a semicolon (;), we check to see if it appears to resemble an entity reference; if the preceding text is & followed by one or more alphanumeric characters. If so, it is excluded from the autolink:
##### Example :
```
www.google.com/search?q=commonmark&hl=en

www.google.com/search?q=commonmark&hl;
```
#### < immediately ends an autolink.
##### Example :
```
www.commonmark.org/he<lp
```
#### An extended url autolink will be recognised when one of the schemes http://, or https://, followed by a valid domain, then zero or more non-space non-< characters according to extended autolink path validation:
##### Example :
```
http://commonmark.org

(Visit https://encrypted.google.com/search?q=Markup+(business))
```
#### An extended email autolink will be recognised when an email address is recognised within any text node. Email addresses are recognised according to the following rules:

- One ore more characters which are alphanumeric, or ., -, _, or +.
- An @ symbol.
- One or more characters which are alphanumeric, or - or _, separated by periods (.). There must be at least one period. The last character must not be one of - or _.
#### The scheme mailto: will automatically be added to the generated link:
##### Example :
```
foo@bar.baz
```
#### + can occur before the @, but not after.
##### Example :
```
hello@mail+xyz.example isn't valid, but hello+xyz@mail.example is.
```
#### ., -, and _ can occur on both sides of the @, but only . may occur at the end of the email address, in which case it will not be considered part of the address:
##### Example :
```
a.b-c_d@a.b

a.b-c_d@a.b.

a.b-c_d@a.b-

a.b-c_d@a.b_
```
___
## ***Disallowed Raw HTML***

#### GFM enables the tagfilter extension, where the following HTML tags will be filtered when rendering HTML output:
- <title>
- <textarea>
- <style>
- <xmp>
- <iframe>
- <noembed>
- <noframes>
- <script>
- <plaintext>
#### Filtering is done by replacing the leading < with the entity &lt;. These tags are chosen in particular as they change how HTML is interpreted in a way unique to them (i.e. nested HTML is interpreted differently), and this is usually undesireable in the context of other rendered Markdown content.

#### All other HTML tags are left untouched.
##### Example :
```
<strong> <title> <style> <em>

<blockquote>
  <xmp> is disallowed.  <XMP> is also disallowed.
</blockquote>
```
___
## ***Table***
#### GFM enables the table extension, where an additional leaf block type is available.
#### Cells in one column don’t need to match length, though it’s easier to read if they are. Likewise, use of leading and trailing pipes may be inconsistent:
##### Example :
```
| abc | defghi |
:-: | -----------:
bar | baz
```
#### Include a pipe in a cell’s content by escaping it, including inside other inline spans:
##### Example :
```
| f\|oo  |
| ------ |
| b `\|` az |
| b **\|** im |
```
#### The table is broken at the first empty line, or beginning of another block-level structure:
##### Example :
```
| abc | def |
| --- | --- |
| bar | baz |
> bar
```
#### The header row must match the delimiter row in the number of cells. If not, a table will not be recognized:
##### Example :
```
| abc | def |
| --- |
| bar |
```
#### The remainder of the table’s rows may vary in the number of cells. If there are a number of cells fewer than the number of cells in the header row, empty cells are inserted. If there are greater, the excess is ignored:
##### Example :
```
| abc | def |
| --- | --- |
| bar |
| bar | baz | boo |
```
___
## ***Task list items***
#### GFM enables the tasklist extension, where an additional processing step is performed on list items.
#### If the character between the brackets is a whitespace character, the checkbox is unchecked. Otherwise, the checkbox is checked.
##### Example :
```
- [x] foo
  - [ ] bar
  - [x] baz
- [ ] bim
```

