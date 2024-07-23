
## Tabelas:

1. **Users:**
	- user_id (PK, Auto-Incremento)
	- email (Text)
	- password (Text)
2. **Content:**
	- content_id (PK, Auto-Incremento)
	- title (Text)
	- autor (Text)
	- desciption (Text)
	- link (Text)
	- media_type (enum: 'Book', 'Podcast', 'Article', 'Video')
	- tags_type (enum: 'Career', 'UX fundamentals', 'Interaction design', 'UI design', 'Information architecture')
	- cover_image (Text)

----
## V2 

> Pensei nessa versão por causa da pesquisa por tags, talves seja mais facil linkar elas dessa forma

1. **Users:**
	- user_id (PK, Auto-Increment)
	- email (Text)
	- password (Text)
2. **Content:**
	- content_id (PK, Auto-Increment)
	- title (Text)
	- autor (Text)
	- desciption (Text)
	- link (Text)
	- media_type (FK)
	- cover_image (Text)
3. **Tags:**
	- tag_id (PK, Auto-Increment)
	- tag_name ('Career', 'UX fundamentals', 'Interaction design', 'UI design', 'Information architecture')
4. **Media:**
	- media_id: (PK, Auto-Incremento)
	- media_type (enum: 'Book', 'Podcast', 'Article', 'Video')
5. **Content_Tags:**
	- content_tag_id (PK, Auto-Incremento)
	- content_id (FK)
	- tag_id (FK)