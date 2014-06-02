Permitiendo la actualización de campos
======================================

El archivo del modelo `app/models/post.rb` es tan simple como:

```ruby
class Post < ActiveRecord::Base
end
```

No hay mucho en ese archivo - pero nota que la clase `Post` hereda de
`ActiveRecord::Base`. Active Record provee una gran cantidad de funcionalidad a los
modelos de Rails de forma sencilla, incluyendo las operaciones básicas CRUD (del
inglés Create, Read, Update, Destroy) de base de datos, validación de datos así
como el soporte a búsquedas sofisticadas y la habilidad de relacionar múltiples
modelos entre sí.

Rails incluye métodos que ayudaran a asegurar los campos de tu modelo.
Abre el archivo `app/models/post.rb` y complétalo de esta manera:

```ruby
class Post < ActiveRecord::Base
  attr_accessible :text, :title
end
```

Este cambio asegura que todos los cambios realizados a través de formularios HTML
puedan editar los campos `text` y `title`.
No será posible definir la edición de otro campo diferente a través de formularios.
Por supuesto aún será posible definirlo usando el método `field=`.
La accesibilidad de los atributos y el problema de la asignación masiva es cubierto
en detalle en [Security guide](http://guides.rubyonrails.org/security.html).
