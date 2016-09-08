Generando un Modelo
===================

Vamos a usar el mismo generador que usamos antes al crear el modelo `Article`. Esta
vez crearemos el modelo `Comment` para los comentarios del artículo. Ejecuta
esto en tu terminal:

```bash
$ rails generate model Comment commenter:string body:text article:references
```

Este comando generará cuatro archivos:

| Archivo                                      | Propósito                                                                                                |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------|
| db/migrate/20140120201010_create_comments.rb | Migración para crear la tabla de comentarios en tu base de datos |
| app/models/comment.rb                        | El modelo Comment.                                                                                       |
| test/models/comment_test.rb                  | Pruebas unitarias para el modelo de comentarios.                                                         |
| test/fixtures/comments.yml                   | Muestras de comentarios para usar de pruebas.                                                            |

Primero, miremos `app/models/comment.rb`:

```ruby
class Comment < ApplicationRecord
  belongs_to :article
end
```

Ésto es muy similar al modelo `Article` que vimos antes. La diferencia es la
línea `belongs_to :article`, que establece una asociación de Active Record.
Aprenderás un poco más sobre asociaciones en la siguiente sección de esta
guía.

La palabra clave (`:references`) utilizada en el comando bash es un tipo estacial
de datos para los modelos. Se crea una nueva columna en la tabla de base de datos
con el nombre del modelo proporcionado con un `_id` que puede contener valores
enteros. Se puede obtener una mejor comprensión después de analizar el archivo
`db/schema.rb` a continuación.

Además del modelo, Rails hizo la migración para crear la tabla correspondiente
en la base de datos:

```ruby
class CreateComments < ActiveRecord::Migration[5.0]
  def change
    create_table :comments do |t|
      t.string :commenter
      t.text :body
      t.references :article, foreign_key: true

      t.timestamps
    end
  end
end
```
La línea de `t.references` crea una columna entera llamada `article_id`, un índice,
y una restricción de `foreign key` que apunta a la columna id de la tabla `articles`.
Corre la migración:

```bash
$ rails db:migrate
```

Rails es suficientemente listo para sólo ejecutar las migraciones que no se han
ejecutado todavía en la base de datos actual, así que en este caso sólo verás:

```bash
==  CreateComments: migrating =================================================
-- create_table(:comments)
   -> 0.0115s
==  CreateComments: migrated (0.0119s) ========================================
```
