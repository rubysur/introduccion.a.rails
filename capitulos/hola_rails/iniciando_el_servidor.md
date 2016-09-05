Iniciando el Servidor Web
=========================

En realidad ya tienes una aplicación Rails funcional, Para verla, necesitas
iniciar un servidor web en tu máquina de desarrollo. Puedes hacerlo ejecutando:

```bash
$ rails server
```

> **TIP:** Compilando CoffeeScript a JavaScript requiere un JavaScript runtime y la
ausencia de éste dará un error de `execjs`. Usualmente Mac OS X y Windows vienen
con un Javascript runtime instalado. Rails agrega la gema `therubyracer` al
`Gemfile` en una línea comentada para nuevas aplicaciones y puedes descomentarla
si la necesitas. `therubyrhino` es el runtime recomendado para usuarios de JRuby
y es añadido por defecto al `Gemfile` en aplicaciones generadas bajo JRuby.
Puedes investigar acerca de todos los runtimes soportados en
[ExecJS](https://github.com/sstephenson/execjs#readme).

Esto lanzará WEBrick, un servidor web incorporado en Ruby por defecto. Para ver
tu aplicación en acción, abre tu navegador preferido e ingresa a [http://localhost:3000](http://localhost:3000).
Deberías ver la página de información por defecto de Rails.

![Welcome Aboard screenshot](http://guides.rubyonrails.org/images/getting_started/rails_welcome.png)

> **TIP:** Para detener el servidor web, presiona Ctrl+C en la ventana de la línea
de comandos donde se está ejecutando. En modo de desarrollo, Rails generalmente
no requiere reiniciar el servidor web; los cambios realizados serán tomados
automáticamente por el servidor.

La página "Welcome Aboard" es la primera prueba para una nueva aplicación Rails:
Ésta asegura que tienes el software configurado correctamente para servir una página.
También puedes hacer click en el link _About your application's enviroment_ para ver
un resumen del entorno de tu aplicación.
