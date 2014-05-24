Mostrando artículos
===================

Si envías el formulario de nuevo, Rails se quejará que no has definido la acción `show`.
Esto no es muy útil así que vamos a agregar la acción `show` antes de continuar. Abra
el archivo `config/routes.rb` y agregue la siguiente ruta:

```ruby
get "posts/:id" => "posts#show"
```

La sintaxis especial `:id` le dice a Rails que la ruta espera un parámetro `:id`,
el cual en nuestro caso será el id del artículo. Note que en esta ocasión
debemos indicar la asignación real `posts#show` porque de otra manera Rails no sabrá
que acción debe realizar.

Como dijimos anteriormente, necesitamos agregar la acción `show` en el `posts_controller`
y su respectiva vista.

```ruby
def show
  @post = Post.find(params[:id])
end
```

Un par de cosas a tener en cuenta. Usamos `Post.find` para encontrar el artículo en el
cual estamos interesados. También usamos una variable de instancia (con el prefijo @)
para contener una referencia al objeto `post`. Hacemos eso porque Rails pasará todas
las variables de instancia a la vista.

Ahora, crea un nuevo archivo `app/view/posts/show.html.erb` con el siguiente contenido:

```html+erb
<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @post.text %>
</p>
```

Finalmente, si vas a
[http://localhost:3000/posts/new](http://localhost:3000/posts/new) serás capaz de
crear un artículo. ¡Inténtalo!

![Show action for posts](http://edgeguides.rubyonrails.org/images/getting_started/show_action_for_posts.png)
