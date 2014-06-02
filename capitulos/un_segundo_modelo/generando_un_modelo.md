Generando un Modelo
===================

Vamos a usar el mismo generador que usamos antes al crear el modelo `Post`. Esta
vez crearemos el modelo `Comment` para los comentarios del artículo. Ejecuta
esto en tu terminal:

```bash
$ rails generate model Comment commenter:string body:text post:references
```

Este comando generará cuatro archivos:

| Archivo                                      | Propósito                                                                                                |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------|
| db/migrate/20100207235629_create_comments.rb | Migración para crear la tabla de comentarios en tu base de datos (en tu caso con un timestamp diferente).|
| app/models/comment.rb                        | El modelo Comment.                                                                                       |
| test/unit/comment_test.rb                    | Pruebas unitarias para el modelo de comentarios.                                                         |
| test/fixtures/comments.yml                   | Muestras de comentarios para usar de pruebas.                                                            |

Primero, miremos `comment.rb`:

```ruby
class Comment < ActiveRecord::Base
  belongs_to :post
  attr_accessible :body, :commenter
end
```

Ésto es muy similar al modelo `post.rb` que vimos antes. La diferencia es la
línea `belongs_to :post`, que establece una asociación de Active Record.
Aprenderás un poco más sobre asociaciones en la siguiente sección de esta
guía.

Además del modelo, Rails hizo la migración para crear la tabla correspondiente
en la base de datos:

```ruby
class CreateComments < ActiveRecord::Migration
  def change
    create_table :comments do |t|
      t.string :commenter
      t.text :body
      t.references :post

      t.timestamps
    end

    add_index :comments, :post_id
  end
end
```

La línea `t.references` establece una columna _foreign key_ para la asociación
entre los dos modelos. La línea `add_index` establece un index para esta columna
de la asociación. Corre la migración:

```bash
$ rake db:migrate
```

Rails es suficientemente listo para sólo ejecutar las migraciones que no se han
ejecutado todavía en la base de datos actual, así que en este caso sólo verás:

```bash
==  CreateComments: migrating =================================================
-- create_table(:comments)
   -> 0.0008s
-- add_index(:comments, :post_id)
   -> 0.0003s
==  CreateComments: migrated (0.0012s) ========================================
```
