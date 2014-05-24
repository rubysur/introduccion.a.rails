Estableciendo la base
=====================

La primera cosa que necesitaremos para crear un nuevo post, es crear un espacio para hacer eso
en nuestra aplicación. Un buen lugar podría ser `/posts/new`. Si tratas de navegar a esa
dirección ahora -- visitando <http://localhost:3000/posts/new> -- Rails te dará un error de
ruteo:

![A routing error, no route matches /posts/new](http://edgeguides.rubyonrails.org/images/getting_started/routing_error_no_route_matches.png)

Esto es porque no en ningún lugar dentro de las rutas para la aplicación -- definidas dentro
de `config/routes.rb` -- que defina esta ruta. Por defecto, Rails no tiene rutas configuradas,
excepto por la ruta `root` que definimos anteriormente, es por esto que tú tendrás que definir
tus rutas cuando las necesites.

Para hacer esto, vas a necesitar crear una ruta dentro de el archivo `config/routes.rb`, en
una nueva línea entre el `do` y el `end` del método `draw`:

```ruby
get "posts/new"
```

Esta ruta es super simple: define una nueva ruta que sólo responderá a peticiones `GET`, y qye
la ruta se encuentra en `posts/new`. Pero como sabe a donde ir sin haber usado la opción
`:to`? Bueno, Rails usa una convención sensible aquí: Rails asumirá que lo que tú quieres
es que esta ruta vaya a la acción `new` dentro de el controlador `posts`.

Con esta ruta definidad, tus peticiones ahora se pueden hacer a través de `/posts/new` en
la aplicación. Navega hacia: <http://localhost:3000/posts/new>. Verás otro error de ruteo:

![Another routing error, uninitialized constant PostsController](http://edgeguides.rubyonrails.org/images/getting_started/routing_error_no_controller.png)

Este error está pasando porque esta ruta necesita un controlador que esté definido. La ruta
está tratando de encontrar el controlador para servir la petición, pero con el controlador
no definido, simplemente no lo puede hacer. La solución para este caso en particular es simple:
crea un controlador llamado `PostsController`. Puedes hacerlo ejecutando el siguiente comando:

```bash
$ rails g controller posts
```

Si abres el nuevo archivo generado `app/controllers/posts_controller.rb`,
verás un controlador vacío:

```ruby
class PostsController < ApplicationController
end
```

Un controlador es simplemente una clase que es definida para heredar de `ApplicationController`.
Dentro de ésta, vas a definir los métodos que se convertirán en acciones para este controlador.
Estas acciones van a ejecutar operaciones _CRUD_ sobre los posts dentro de nuestro sistema.

Si refrescas la dirección <http://localhost:3000/posts/new> ahora, vas a tener un nuevo error:

![Unknown action new for PostsController!](http://edgeguides.rubyonrails.org/images/getting_started/unknown_action_new_for_posts.png)

Este error indica que Rails no puede encontrar la acción `new` dentro de
`PostsController` que recién has generado. Esto es porque cuando los controladores
son generados en Rails están vacíos por defecto, a menos que le digas que acciones
quieres durante el proceso de generación.

Para definir manualmente una acción dentro de un controlador, todo lo que necesitas
es definir un nuevo método dentro del controlador. Abre `app/controllers/posts_controller.rb`
y dentro de la clase `PostsController`, define el método `new` así:

```ruby
def new
end
```

Con el método `new` definido en `PostsController`, si tú refrescas
<http://localhost:3000/posts/new> verás otro error:

![Template is missing for posts/new](http://edgeguides.rubyonrails.org/images/getting_started/template_is_missing_posts_new.png)

Estás obteniendo este error ahora porque Rails espera que las acciones planas
como ésta tengan vistas asociadas a ellas para mostrar la información. Con ninguna
vista disponible, Rails mostrará un error.

En la imagen de arriba, la línea de abajo fue eliminada. Vamos a ver como se ve el error completo:

<blockquote>
Missing template posts/new, application/new with {:locale=>[:en], :formats=>[:html], :handlers=>[:erb, :builder, :coffee]}. Searched in: * "/path/to/blog/app/views"
</blockquote>

Eso es casi un montón de texto! Revisemos rápidamente para entender cuál es la función de cada parte.

La primera parte identifica que plantilla está faltando. En este caso, es la plantila `posts/new`.
Rails primero buscará esta plantilla. Si no la encuentra, luego tratará de cargar la plantilla
llamada `application/new`. Busca una aquí porque el `PostsController` hereda de `ApplicationController`.

La siguiente parte del mensaje contiene un map (`hash` en inglés). La llave `:locale` en este map
simplemente indica el lenguaje que debe contener la plantilla solicitada. Por defecto, está configurado
en Inglés -- o "en" --. La siguiente llave, `:formats` especifica el formato de la plantilla que será
servido en la respuesta. El formato por defecto es `:html`, es por eso que Rails busca una plantilla
HTML. La llave final, `:handlers`, nos dice que _manejador de plantilla_ (o _template handler_ en inglés)
puede ser usada para producir nuestra plantilla. `:erb` es el manejador más usado para plantillas HTML,
`:builder` es usado para plantillas XML, y `:coffee` usa CoffeeScript para construir plantillas JavaScript.

La más simple plantilla que funcionaría en nuestro caso sería una localizada en `app/views/posts/new.html.erb`.
La extensión de este nombre de archivo es importante: la primera extensión define el _formato_ de la plantilla,
y la segunda extensión el _manejador de plantilla_ que será usado. Rails está tratando de encontrar una
plantilla llamada `posts/new` en `app/views` para la aplicación. El formato para esta plantilla puede sólo
ser `html` y el manejador debería ser `erb`, `builder` o `coffee`. Ya que tú quieres crear un nuevo
formulario HTML, tú tendrás que usar el lenguaje `ERB`. Por lo tanto el archivo debería ser llamado
`posts/new.html.erb` y necesita ser localizado dentro de la carpeta `app/views` de la aplicación.

Ahora ve y crea un nuevo archivo en `app/views/posts/new.html.erb` y escribe el siguiente
contenido en él:

```html
<h1>New Post</h1>
```

Cuando refresques <http://localhost:3000/posts/new>, verás que la página tiene un título. La ruta,
el controlador, la acción y la vista ahora están funcionando de manera armoniosa! Es hora de crear
el formulario para un nuevo post.
