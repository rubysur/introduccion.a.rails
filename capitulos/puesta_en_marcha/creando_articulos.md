Creando artículos
=================

Para hacer que "Unknown action" desaparezca, puedes definir una acción `create`
dentro de la clase `ArticleController` en `app/controllers/articles_controller.rb`, debajo de la acción `new`:

```ruby
class ArticlesController < ApplicationController
  def new
  end

  def create
  end
end
```
Si reenvias el formulario ahora no veras ningun cambio en la pagina. Esta bien, esto es porque Rails
por defecto devuelve `204 No Content` a una acción si no se especifica cuál debe ser la respuesta.
Añadimos la accion `create` pero no especificamos cual debe ser la respuesta. En este caso, la acción `create` debe salvar el nuevo artículo en la base de datos.

Cuando un formulario es enviado, los campos del formulario son enviados a Rails como _parámetros_. Estos
parámetros pueden ser referenciados dentro de las acciones del controlador, generalmente para realizar una
tarea determinada. Para ver qué hacen estos parámetros, cambiar la acción `create` a esto:

```ruby
def create
  render plain: params[:article].inspect
end
```

El método `render` toma un simple hash con la clave `:plain` y el valor de `params[:post].inspect`. El
método `params` es el objeto que representa a los parámetros (o campos) que vienen desde el formulario.
El método `params` retorna un objeto `ActionController::Parameters`, que te permite acceder a las claves del hash
usando cadenas o símbolos. En esta situación, los únicos parámetros que importan son los que vienen del
formulario.

Si reenvías el formulario una vez más, ya no obtendrás el error de plantilla faltante, en su lugar verás
algo como lo que sigue:

```ruby
<ActionController::Parameters {"title"=>"First Article!", "text"=>"This is my first article."} permitted: false>
```

Esta acción muestra ahora los parámetros para el artículo que están llegando desde el formulario. Sin
embargo, esto no es realmente útil. Sí, puedes ver los parámetros, pero no hay nada en particular que se
está haciendo con ellos.
