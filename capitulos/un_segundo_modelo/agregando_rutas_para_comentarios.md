Agregando una Ruta para Comentarios
===================================

Así como con el controlador `welcome`, vamos a necesitar agregar una ruta para
que Rails sepa donde queremos navegar para ver `comments`. Abre el archivo
`config/routes.rb`, y edítalo de la siguiente manera:

```ruby
resources :articles do
  resources :comments
end
```

Esta configuración crea la ruta `comments` dentro de la ruta `articles` que definimos
anteriormente. Esta es otra forma de establecer la relación entre los dos modelos.

SUGERENCIA: Para más información sobre el ruteo, mira la guía
[Rails Routing from the Outside In](http://guides.rubyonrails.org/routing.html)
(en inglés).
