Seguridad
=========

Si fueras a publicar tu blog en línea, cualquier persona podría agregar, editar
y eliminar artículos o eliminar comentarios.

Rails provee un sistema muy simple de autenticación por HTTP que funcionaría muy
bien en esta situación.

Necesitamos una forma de bloquear el acceso a ciertas acciones en el controlador
`ArticlesController` si la persona no está autenticada, aquí podemos usar el método
de Rails `http_basic_authenticate_with`, que permite acceso a la acción
solicitada si el método retorna `true`.

Para usar el sistema de autenticación, lo especificamos en la parte inicial de
`ArticlesController`, en este caso, queremos autenticar al usuario en cada una de
las acciones, excepto `index` y `show`, así lo escribimos:

```ruby
class ArticlesController < ApplicationController

  http_basic_authenticate_with name: "dhh", password: "secret", except: [:index, :show]

  def index
    @articles = Article.all
  end
# cortado por brevedad
```

También queremos limitar la eliminación de comentarios a los usuarios autenticados, así
que en `CommentsController` (`app/controllers/comments_controller.rb`) escribimos:

```ruby
class CommentsController < ApplicationController

  http_basic_authenticate_with name: "dhh", password: "secret", only: :destroy

  def create
    @article = Article.find(params[:article_id])
    # ...
  end
# cortado por brevedad
```

Ahora si intentas crear un nuevo artículo, vas a ser recibido con una ventana
de diálogo de autenticación HTTP básica.

![Ventana de diálogo de autenticación HTTP básica](http://guides.rubyonrails.org/images/getting_started/challenge.png)

Hay otros metodos de autentificacion disponibles para aplicaciones Rails.
Dos de los mas gemas mas populares para Rails son Devise y Authlogic, junto con muchas mas.

Otros comentarios sobre la seguridad
------------------------------------

La seguridad, sobre todo cuando habamos de aplicaciones web, es un tema muy complejo.
Por eso puedes consultar la guía [Ruby on Rails Security Guide](http://guides.rubyonrails.org/security.html) para obtener más información al respecto.
