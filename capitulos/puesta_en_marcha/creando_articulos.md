Creando artículos
=================

Para hacer que "Unknown action" desaparezca, puedes definir una acción `create`
dentro de la clase `PostsController` en `app/controllers/posts_controller.rb`, debajo de la acción `new`:

```ruby
class PostsController < ApplicationController
  def new
  end

  def create
  end
end
```

Si reenvías el formulario ahora, verás otro error común: falta una plantilla. Está bien, vamos a ignorar
eso por ahora. Lo que la acción `create` debe hacer es salvar el nuevo artículo en la base de datos.

Cuando un formulario es enviado, los campos del formulario son enviados a Rails como _parámetros_. Estos
parámetros pueden ser referenciados dentro de las acciones del controlador, generalmente para realizar una
tarea determinada. Para ver qué hacen estos parámetros, cambiar la acción `create` a esto:

```ruby
def create
  render :text => params[:post].inspect
end
```

El método `render` toma un simple hash con la clave `text` y el valor de `params[:post].inspect`. El
método `params` es el objeto que representa a los parámetros (o campos) que vienen desde el formulario.
El método `params` retorna un objeto `HashWithIndifferentAccess`, que te permite acceder a las claves del hash
usando cadenas o símbolos. En esta situación, los únicos parámetros que importan son los que vienen del
formulario.

Si reenvías el formulario una vez más, ya no obtendrás el error de plantilla faltante, en su lugar verás
algo como lo que sigue:

```ruby
{"title"=>"First post!", "text"=>"This is my first post."}
```

Esta acción muestra ahora los parámetros para el artículo que están llegando desde el formulario. Sin
embargo, esto no es realmente útil. Sí, puedes ver los parámetros, pero no hay nada en particular que se
está haciendo con ellos.
