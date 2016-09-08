Eliminando Objetos Asociados
============================

Si borras un artículo, todos sus comentarios también derían borrarse para que no
ocupen un espacio innecesario en la base de datos. Rails permite configurar este
comportamiento mediante la opción `dependent` de la asociación entre modelos.
Para ello, modifica el modelo `Article` cambiando el contenido del archivo
`app/models/article.rb` por lo siguiente:

```ruby
class Article < ApplicationRecord
  has_many :comments, dependent: :destroy
  validates :title, presence: true,
                    length: { minimum: 5 }
end
```
