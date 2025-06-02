## Bold Text
for bold - **bold txt**



## Italics
*italics*


## Underline
_underline_

## Links
this is link - use command + k for the link part 

How to create a link? - Write the title of the page and surround it with square brackets to create a link to the new note. If note doesn't exist a new note is created. If exists, you can use that name to link it to that particular note.

Can also reference specific headings within a note - To highlight a particular section of the note.

If you want to reference a heading, then use double [] and then # after writing a the page name to reference the heading in that page.
If you want to reference the content of the section as well, then use ! before the double [] to display that section of the note which is being referenced in the current note.
If you want to link only a specific paragraph, then use carrot symbol (^) to highlight and display on specific sections of that note here as well. 
Note: This works with hierarchy, that is reference page title -> then headings or individual sections within that page. 

## Headings 
For creating a heading use #
eg - 
### Heading1
#### heading 2
Note: Headings get nested to the previous larger heading.

If writing a current note and want to create a separate note for it, then highlight, right click and extract selection - then you can create a new note for that section in this way.

## Hashtags
Using hashtags helps to creates tag that ease up searching, if its a concept but not necessarily present separately in a note. 
#example-tag this is an example hashtag to show the working of tags which show in search with the text near them.

Note: This space separated part also show up in the search though, hence it refers to the paragraph associated with the hashtag. However section after next heading don't.

Hashtags can also be nested eg - tagA/tagB nests tagA under tagB

## Hashtags vs Links
Hashtags - basically for searching purposes. However links are for reusability. Don't create too broad hashtags,  essentially should point to what they reference for search-abilty.
Links - topics, concepts, research articles
Hashtags - categories **with intent**

## Searching in Obsidian
Command + shift + F for quick access 
if you want to search with and -> wordA wordB
if you want or -> wordA OR wordB
if you want to exclude the second word as string which could be a substring of another word too -> wordA - wordB
if you want top exclude purely only the word as a whole not it as a substring of other words -> wordA -"wordB"
if you want to open the search document in new pane -> cmd + click
can also drag from search to insert that as a link to another note.

Use () for expressions you want to search as an expression.
eg. If i am searching in section: (/\d\d% paddy) -> this will find out occurrence of double digit percentage with paddy in the same section.
### Regex Search
\d -> digit
\w ->word
\W -> anything not a word
\s -> space 
if you use plus(+) after any above symbol -> means 1 or more
if you use (?) or star  after any above symbol -> means 0 or more
For more RegEX stuff -> [Website for learning RegEx](https://automatetheboringstuff.com)
To start using RegEx search in obsidian -> / then RegEx Expression ending with another / 
say you wanna search exactly 4 digits -> \d{4}
Use back-ward slash (\) as escape character if you wanna search the special characters of RegEx 
eg. -> \? will escape it and search for it.
















