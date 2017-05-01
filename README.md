# Collate File Format
The following document specifies Collate's file format.

Collate's file format optimizes for human readability.  The goal is a format which can be easily parsed and read without the aid of software other than a file browser and text editor.  This is important for long term archival purposes as well as removing anxiety about being "locked-in" to a developer's ecosystem.  There is a comfort in knowing that your data will be safe and available to you no matter what happens.

## File structure

Collate's file structure is very simple. Here is an example file structure:

	Collection
	|-- Inbox
	|   `-- Welcome
	|       |-- welcome.md
	|       `-- attachments
	|           `-- attachment.jpg
	|-- Todo
	|   `-- January 1 2017
	|       |-- january 1 2017.md
	|       `-- attachments
	|           `-- presentation.doc
	`-- Recipes
	    `-- Hot dogs au gratin
	        |-- hot dogs au gratin
	        `-- attachments
	            `-- Hot dog recipe.pdf


## Collection

A Collection is a directory where everything is stored. Its located anywhere the user has access.  There are no naming conventions or restrictions.

## Notebooks

A Notebook is any directory directly nested under the main Collection directory.

_The naming convention was removed 4/27/2017._
_Going forward, Collate will still read notes and notebooks with the old format and will not convert them. However, any new notes and notebooks will not be constrained._

A notebook is any directory immediately nested under the main Collection.

## Notes

A note is any directory directly nested under a notebook and second child of the Collection directory

_The naming convention was removed 4/27/2017._
_Going forward, Collate will still read notes and notebooks with the old format and will not convert them. However, any new notes and notebooks will not be constrained._

## Note Files

A Note File is a markdown file with suffix `.md` which is nested immediately under a Note.

_The naming convention was removed 4/27/2017._

A note file has two parts, the frontmatter containing the machine readable metadata and the note body which contains the contents of the note.

### Frontmatter
Collate uses [YAML](http://yaml.org/) formatted front matter to store note metadata as inspired by [Jekyll](https://jekyllrb.com/docs/frontmatter/).  YAML offers a great readable way to store metadata for Notes.

Collate's YAML frontmatter looks like this:

```
---
title: Anatomy of a Collate Note
tags:
  - Collate
  - Markdown
  - YAML
type: markdown
created: 2017-02-16T08:51:20.000Z
modified: 2017-02-16T08:56:56.000Z
---
```

Translated to JSON:

```
{
	"title": "Anatomy of a Collate Note",
	"tags": ["Collate", "Markdown", "YAML"],
	"type": "markdown",
	"created": "2017-02-16T08:51:20.000Z",
	"modified": "2017-02-16T08:56:56.000Z"
}
```
The only required key is the title.

Here's a table of keys:

| Key         	| Required/Optional 	| Data Type 	| Default Value	|
|-------------	|-------------------	|-----------	|--------------	|
| title       	| Required          	| String    	|		|
| tags        	| Optional          	| Array     	| 		|
| type		| Optional		| String	| markdown	|
| created	| Optional		| String	|		|
| modified	| Optional		| String	|		|

Created and Modified use ISO 8601 formatted strings. If not found, Collate defaults to system birthtime for created and mtime for modified.

Other fields may also be added to the frontmatter and Collate may utilize it in the future for other features.

**Note: Any additional YAML encoded fields in the front matter will be passed through by Collate.**

### Body

The default body text is in markdown format.  

Collate will use [Github Flavored Markdown](https://guides.github.com/features/mastering-markdown/#GitHub-flavored-markdown), a superset of Markdown which includes [CommonMark](http://commonmark.org/).

As of v. 0.2.3, Collate will be expanding the contents of the body to include other types of data in support of the upcoming Note Types feature. This feature trades rich text or other note editing capabilities on the front end of the application for a less readable but more flexible data format. Data types may include JSON, HTML, or additional types in the future.  Files that contain data other than markdown must be denoted in the front matter by using the type key.  


## Attachments

The attachments folder may hold any type of file.  Collate will not open or parse these files except for the file name.  Any directories within this folder will be ignored, but this may change in the future.
