Creando el modelo Article
======================

Los modelos en Rails usan un nombre en singular, y sus correspondientes tablas
de base de datos usan un nombre en plural. Rails provee un generador para crear
modelos, el cual la mayoría de desarrolladores en Rails tienden a usar para
crear nuevos modelos. Para crear un nuevo modelo, ejecuta este comando en tu
terminal:

```bash
$ rails generate model Article title:string text:text
```

Con ese comando le decimos a Rails que nosotros queremos un modelo `Article`,
junto con un atributo _title_ de tipo _string_, y un atributo _texto_ de tipo
_text_. Esos atributos son automáticamente añadidos a la tabla `articles` en la
base de datos y mapeados al modelo `Article`.

Rails respondió con la creación de un montón de archivos. Por ahora, nosotros
sólo estamos interesados en `app/models/article.rb` y
`db/migrate/20140120191729_create_articles.rb` (en tu caso puede ser un poco
diferente). Este último es responsable de crear la estructura de la base
de datos, que es lo que revisaremos luego.

> **TIP:** Active Record es lo suficientemente inteligente para asignar
automáticamente el nombre de las columnas a atributos del modelo,
lo que significa que tú no tienes que declarar los atributos dentro
de los modelos de Rails, ya que será realizado automáticamente por
Active Record.
