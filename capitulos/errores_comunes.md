Errores comunes de configuración
================================

La forma más fácil de trabajar con Rails es guardando toda los datos externos
como UTF-8. Si no lo haces, por lo general las librerías de Ruby y Rails van a
ser capaces de convertir tus datos nativos a UTF-8, pero esto no funciona en
todos los casos, así que lo ideal es asegurarte que todos tus datos externos
usen UTF-8.

Si has cometido un error de este tipo, el síntoma más común es un símbolo de un
diamante negro con un signo de interrogación en vez de algunos caracteres en tu
navegador. Otro síntoma común es ver caracteres como "Ã¼" apareciendo en vez de
la "ü" por ejemplo. Rails realiza una serie de pasos internos para resolver
casos comunes. Sin embargo, si tienes datos externos que no están guardados en
UTF-8, puede resultar en este tipo de problemas al no ser automáticamente
detectados y resueltos por Rails.

Dos fuentes comunes de datos que no están en UTF-8:

* Tu editor de texto: La mayoría de editores de texto (como TextMate, o Sublime
  Text), guardan los archivos en UTF-8 por defecto. Si tu editor no lo hace,
  esto puede resultar en los problemas mencionados arriba. Esto también aplica
  a los archivos de traducción para I18n. La mayoría de editores que no usan
  UTF-8 por defecto (como algunas versionesde Dreamweaver) ofrecen una manera
  para cambiar la opción por defecto a UTF-8. Házlo!
* Tu base de datos. Rails convierte los datos que intercambia con tu base de
  datos a UTF-8 por defecto. Sin embargo, si tu base de datos no está usando
  UTF-8 internamente, puede no ser capaz de guardar todos los datos que ingresen
  tus usuarios. Por ejemplo, si tu base de datos está usando Latin-1
  internamente, y tus usuarios ingresan caracteres rusos, hebreos o japoneses,
  esos datos serán perdidos para siempre una vez que entren a la base de datos.
  Si es posible, usa UTF-8 internamente para el almacenamiento de datos.
