Mostrando artículos
===================

Si envías el formulario de nuevo, Rails se quejará de que no has definido la acción `show`.
Esto no es muy útil así que vamos a agregar la acción `show` antes de continuar.

Como viste en la salida del comando `rails routes`, la ruta de la acción `show` tiene este aspecto:

```bash
article GET    /articles/:id(.:format)      articles#show
```

La sintaxis `:id` de la ruta indica a Rails que esta ruta espera un parámetro llamado `:id`, que en este caso será el atributo id del artículo que se quiere ver.

Como hicimos anteriormente, es necesario añadir una nueva acción en el archivo `app/controllers/articles_controller.rb` y también hay que crear su vista correspondiente.

Vamos a añadir la acción show, de la siguiente manera:

```ruby
class ArticlesController < ApplicationController
  def show
    @article = Article.find(params[:id])
  end

  def new
  end
```
Un par de cosas que debes tener en cuenta: usamos `Article.find` para encontrar el artículo que nos interesa, pasándole el valor `params[:id]` para obtener el parámetro `:id` directamente de la petición. También usamos una variable de instancia (con el prefijo @) para guardar una referencia al objeto del artículo. Hacemos eso porque Rails pasa automáticamente todas las variables de instancia a la vista.

Ahora, crea un nuevo archivo `app/view/articles/show.html.erb` con el siguiente contenido:

Abre el archivo `config/routes.rb` y agrega la siguiente ruta:

```ruby
<p>
  <strong>Title:</strong>
  <%= @article.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @article.text %>
</p>
```

Finalmente, si vas a
[http://localhost:3000/posts/new](http://localhost:3000/articles/new) serás capaz de
crear un artículo. ¡Inténtalo!

![Show action for posts](http://guides.rubyonrails.org/images/getting_started/show_action_for_articles.png)
