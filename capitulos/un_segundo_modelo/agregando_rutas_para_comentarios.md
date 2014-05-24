Agregando una Ruta para Comentarios
===================================

Así como con el controlador `welcome`, vamos a necesitar agregar una ruta para
que Rails sepa donde queremos navegar para ver `comments`. Abre el archivo
`config/routes.rb` nuevamente, y edítalo de la siguiente manera:

```ruby
resources :posts do
  resources :comments
end
```

Ésto crea `comments` como un _recurso anidado_ dentro de `posts`. Esta es otra
parte de capturar la relación jerárquica que existe entre artículos y
comentarios.

SUGERENCIA: Para más información sobre el ruteo, mira la guía
[Rails Routing from the Outside In](http://guides.rubyonrails.org/routing.html)
(en inglés).
