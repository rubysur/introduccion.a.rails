Asociando Modelos
=================

Las asociaciones de Active Record te permiten declarar fácilmente la relación
entre dos modelos. En el caso de los comentarios y artículos, puedes escribir la
relación de esta manera:

* Cada comentario pertence a un artículo.
* Un artículo puede tener muchos comentarios.

De hecho, ésto es muy cercano a la sintáxis que usa Rails para declarar esta
asociación. Ya has visto la línea de código en el modelo `Comment` que hace que
cada comentario pertenezca a un artículo:

```ruby
class Comment < ActiveRecord::Base
  belongs_to :post
end
```

Vas a tener que editar el archivo `post.rb` para agregar el otro lado de la
asociación:

```ruby
class Post < ActiveRecord::Base
  validates :title, :presence => true,
                    :length => { :minimum => 5 }

  has_many :comments
end
```

Estas dos declaraciones permiten bastante comportamiento automatizado. Por
ejemplo, si tienes una variable de instancia `@post` conteniendo un artículo,
puedes obtener todos los comentarios que pertenecen a ese artículo como un
arreglo usando `@post.comments`.

SUGERENCIA: Para más información sobre las asociaciones de Active Record, revisa
la guía [Active Record Associations](http://guides.rubyonrails.org/association_basics.html)
(en inglés).
