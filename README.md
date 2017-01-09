# Collate File Format
The following document specifies Collate's file format.

Collate's file format optimizes for readability and openness above all other attributes.  The goal is to have a human readable format which can be easily parsed and read without the aid of software.  This is important for long term archival purposes as well as removing anxiety about being "locked-in" to a developer's ecosystem.  There is a comfort in knowing that your data will be safe and available to you no matter what happens.

## File structure

Collate's file structure is very simple.  

A Collection is a directory where everything is stored.

A Notebook is a directory with a `.notebook` suffix and is nested immediately under a Collection.  Notebooks have a strict file naming convention.  They can only contain the characters `a-zA-Z0-9-` (alpha-numeric characters and the character "-").  Spaces are not allowed.

Valid: `This-is-a-notebook-1234.notebook`
Invalid: `This is a notebook.notebook`
Invalid: `This_is_a_notebook.notebook`
Invalid: `This-is-a-notebook!.notebook`

A Note is a directory with a `.note` suffix and is nested immediately under a Notebook.  Notes have the same strict file naming convention as notebooks.  They must only contain the characters `a-zA-Z0-9-`.

A Note File is a markdown file with suffix `.md` which is nested immediately under a Note.  As convention, Collate names Note files the same as notes, just with a `.md` extension instead of `.note`.

Attachments within a note are stored in an attachments directory.  Attachment directories are located immediately under a Note.  They must be named attachment, and are optional.  If there are no attachments, the attachment directory does not need to exist.  Attachments located inside the attachment folder may be of any type.  Collate ignores directories within the attachments directory, but may support reading them as a flat structure in the future.


Here is an example file structure:

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



## Notebooks



## Notes


## Note Markdown Files

### Frontmatter


### Body



## Attachments
