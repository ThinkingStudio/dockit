# Dockit API

This page documents DocKit API specification

## Context

There are two configurable URL contexts used in Dockit:

1. editor - the editor context, used to load dockit application files, default value is `/editor`
2. doc - the document/image context, used to load editing target files, default value is `/doc`

## Endpoints

### `GET /editor/config`

Retrieve the dockit configuration. Sample response:

```json
{
	"repoUrl": "/doc",
	"imgPath":" /img"
}
```

**Note** the full image context is `${repoUrl}${imagePath}`

### `GET /doc`

Get the root level document/folder list. Sample response:

```json
[
	{
		"path": "",
		"label": ".",
		"isFolder": true
	},
	{
		"path": "/api.md",
		"isFolder": false
	}
]
```

### `GET /doc/{path}`

Get the resource specified by path, where the resource could be either a markdown file or a folder. E.g. `/doc/api.md` or `/doc/path/to/folder`. 

When resource specified by path is a markdown file, then this endpoint shall return the content of the file

When resource specified by path is a folder, then this endpoint shall return a JSON array contains the direct markdown files or sub folders contained in the folder specified. Refer to the sample response specified in above endpoint: `GET /doc`

### `POST /doc/{path-to-md}`

Save a content of the current editor buffer to a markdown file specified by `${path-to-md}`. E.g. `POST /doc/tutorial/step1.md`

The payload shall be the editor buffer content.



