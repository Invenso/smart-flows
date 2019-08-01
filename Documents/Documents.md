#Documents

Api used to preview documents, get document information & content.

#### GET /api/v1/documents/{documentId}
Get document information like name, content type, created date,...

#### GET /api/v1/documents/{documentId}/content
Get the binary content of the document

#### POST /api/v1/documents
Create a preview of a document using (a) sample(s) in different output formats (docx, pdf or html)

Example payload template with 2 datasets. This will result in an html-document.

```
{
	"dataRefs": [
		sample-id-for-dataset-1,
		sample-id-for-dataset-2
	],
	"language": "en",
	"templateRef": {
		"id": "id-for-template"
	},
	"result": {
		"format": "html"
	}
}
```