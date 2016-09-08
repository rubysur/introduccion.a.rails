Estableciendo la base
=====================

La primera cosa que necesitaremos para crear un nuevo post, es crear un espacio
en nuestra aplicación. Un buen lugar podría ser `/articles/new`. Si tratas de navegar a esa
dirección ahora -- visitando <http://localhost:3000/articles/new> -- Rails te dará un error de
ruteo:

![A routing error, no route matches /articles/new](http://guides.rubyonrails.org/images/getting_started/routing_error_no_controller.png)

Este error se produce porque la ruta tiene que tener un controlador definido con el fin de atender la solicitud. La solución a este problema es simple: crear un controlador llamado `ArticlesController`.Podemos hacer esto mediante la ejecución de este comando:

```bash
rails generate controller Articles
```

Si abres el nuevo archivo generado `app/controllers/articles_controller.rb`,
verás un controlador vacío:

```ruby
class ArticlesController < ApplicationController
end
```

Un controlador es simplemente una clase que es definida para heredar de `ApplicationController`.
Dentro de ésta, vas a definir los métodos que se convertirán en acciones para este controlador.
Estas acciones van a ejecutar operaciones _CRUD_ sobre los posts dentro de nuestro sistema.

Si refrescas la dirección <http://localhost:3000/articles/new> ahora, vas a tener un nuevo error:

![Unknown action new for PostsController!](http://guides.rubyonrails.org/images/getting_started/unknown_action_new_for_articles.png)

Este error indica que Rails no puede encontrar la acción `new` dentro de
`ArticlesController` que recién has generado. Esto es porque cuando los controladores
son generados en Rails están vacíos por defecto, a menos que le digas que acciones
quieres durante el proceso de generación.

Para definir manualmente una acción dentro de un controlador, todo lo que necesitas
es definir un nuevo método dentro del controlador. Abre `app/controllers/articles_controller.rb`
y dentro de la clase `ArticlesController`, define el método `new` así:

```ruby
class ArticlesController < ApplicationController
  def new
  end
end
```

Con el método `new` definido en `ArticlesController`, si actualizas
<http://localhost:3000/articles/new> verás otro error:

![Template is missing for posts/new](http://guides.rubyonrails.org/images/getting_started/template_is_missing_articles_new.png)

Estás obteniendo este error ahora porque Rails espera que las acciones planas
como ésta tengan vistas asociadas a ellas para mostrar la información. Con ninguna
vista disponible, Rails mostrará un error.

En la imagen de arriba, la línea de abajo fue eliminada. Vamos a ver como se ve el error completo:

<blockquote>
ArticlesController#new is missing a template for this request format and variant. request.formats: ["text/html"] request.variant: [] NOTE! For XHR/Ajax or API requests, this action would normally respond with 204 No Content: an empty white screen. Since you're loading it in a web browser, we assume that you expected to actually render a template, not… nothing, so we're showing an error to be extra-clear. If you expect 204 No Content, carry on. That's what you'll get from an XHR or API request. Give it a shot.
</blockquote>

Eso es casi un montón de texto! Revisemos rápidamente para entender cuál es la función de cada parte.

La primera parte identifica que plantilla está faltando. En este caso, es la plantila `articles/new`.
Rails primero buscará esta plantilla, si no la encuentra, tratará luego de cargar la plantilla
llamada `application/new`. Busca una aquí porque el `ArticlesController` hereda de `ApplicationController`.

La siguiente parte del mensaje contiene un map (`hash` en inglés). La clave `:locale` en este map
simplemente indica el lenguaje que debe contener la plantilla solicitada. Por defecto, está configurado
en Inglés -- o "en" --. La siguiente clave, `:formats` especifica el formato de la plantilla que será
servido en la respuesta. El formato por defecto es `:html`, es por eso que Rails busca una plantilla
HTML. La clave final, `:handlers`, nos dice que _manejador de plantilla_ (o _template handler_ en inglés)
puede ser usada para producir nuestra plantilla. `:erb` es el manejador más usado para plantillas HTML,
`:builder` es usado para plantillas XML, y `:coffee` utiliza CoffeeScript para construir plantillas JavaScript.

El mensaje también contiene `request.formats` que especifica el formato de la plantilla que se sirve en la respuesta. Se establece `text/html` como solicitamos esta página a través del navegador, por lo que Rails está buscando una plantilla HTML.

La más simple plantilla que funcionaría en nuestro caso sería una localizada en `app/views/articles/new.html.erb`. La extensión de este nombre de archivo es importante: la primera extensión define el _formato_ de la plantilla, y la segunda extensión el _manejador de plantilla_ que será usado. Rails está tratando de encontrar una plantilla llamada `articles/new` en `app/views` para la aplicación. El formato para esta plantilla puede sólo ser `html` y el manejador debería ser `erb`, `builder` o `coffee`.

Ya que tú quieres crear un nuevo formulario HTML, tendrás que usar el lenguaje `ERB`. Por lo tanto el archivo debería ser llamado `articles/new.html.erb` y necesita ser localizado dentro de la carpeta `app/views` de la aplicación.

Ahora ve y crea un nuevo archivo en `app/views/articles/new.html.erb` y escribe el siguiente
contenido en él:

```html
<h1>New Article</h1>
```

Cuando refresques <http://localhost:3000/articles/new>, verás que la página tiene un título. La ruta,
el controlador, la acción y la vista ahora están funcionando de manera armoniosa! Es hora de crear
el formulario para un nuevo post.
