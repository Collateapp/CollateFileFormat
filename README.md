# Collate File Format
The following document specifies Collate's file format.

Collate's file format optimizes for human readability.  The goal is a format which can be easily parsed and read without the aid of software other than a file browser and text editor.  This is important for long term archival purposes as well as removing anxiety about being "locked-in" to a developer's ecosystem.  There is a comfort in knowing that your data will be safe and available to you no matter what happens.

## File structure

Collate's file structure is very simple. Here is an example file structure:

	Collection
	|-- Inbox.notebook
	|   `-- Welcome.note
	|       |-- welcome.md
	|       `-- attachments
	|           `-- attachment.jpg
	|-- Todo.notebook
	|   `-- January-1-2017.note
	|       |-- january-1-2017.note
	|       `-- attachments
	|           `-- presentation.doc
	`-- Recipes.notebook
	    `-- Hot-dogs-au-gratin.note
	        |-- hot-dogs-au-gratin.md
	        `-- attachments
	            `-- Hot dog recipe.pdf


## Collection

A Collection is a directory where everything is stored. Its located anywhere the user has access.  There are no naming conventions or restrictions.

## Notebooks

A Notebook is a directory with a `.notebook` suffix and is nested immediately under a Collection. They can only contain the characters `a-zA-Z0-9-` (alpha-numeric characters and the character "-").  Spaces are not allowed. It must end in `.notebook`.  For example: `Moms-recipes.notebook` or `99-bottles-of-beer.notebook`.

Valid: `This-is-a-notebook-1234.notebook`
Invalid: `This is a notebook.notebook`
Invalid: `This_is_a_notebook.notebook`
Invalid: `This-is-a-notebook!.notebook`

## Notes

Notes are directories and direct children of Notebooks.  Like Notebooks, directory names may only contain alpha-numeric characters a-zA-Z0-9 and the hyphen `-` character.  It must end in `.note`.  For example: `Holiday-shopping-list.note` or `10-places-to-visit.note`.

## Note Files

A Note File is a markdown file with suffix `.md` which is nested immediately under a Note.  As convention, Collate names Note files the same as notes, just with a `.md` extension instead of `.note`.

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

### Body

The default body text is in markdown format.  

Collate will use [Github Flavored Markdown](https://guides.github.com/features/mastering-markdown/#GitHub-flavored-markdown), a superset of Markdown which includes [CommonMark](http://commonmark.org/).

As of v. 0.2.3, Collate will be expanding the contents of the body to include other types of data in support of the upcoming Note Types feature. This feature trades rich text or other note editing capabilities on the front end of the application for a less readable but more flexible data format. Data types may include JSON, HTML, or additional types in the future.  Files that contain data other than markdown must be denoted in the front matter by using the type key.  


## Attachments

The attachments folder may hold any type of file.  Collate will not open or parse these files except for the file name.  Any directories within this folder will be ignored, but this may change in the future.
