# Plugin "Conquer With Words"

El siguiente plugin es un plugin de WordPress que permite a los usuarios de WordPress crear un post con un título y un contenido, y que el contenido sea analizado por el plugin para determinar si el contenido es positivo o negativo.

## ¿Cómo funciona?

El plugin utiliza dos arrays, uno corresponde a las palabras malsonantes y el otro a las palabras positivas. El plugin analiza el contenido del post y cuenta cuantas palabras malsonantes y positivas hay en el contenido. Si hay más palabras malsonantes que positivas, el plugin devuelve un mensaje de error y no permite publicar el post.

- **Función de "renym_wordpress_typo_fix":**

    Esta función toma un parámetro "$text", que se supone es el contenido del post o la página del WP. Dentro de esta, reemplazamos las palabras consideradas ofensivas por un asterisco. Para esto, utilizamos la función "str_replace" de PHP, que toma tres parámetros: el primero es la palabra que queremos reemplazar, el segundo es la palabra por la que queremos reemplazarla y el tercero es el texto en el que queremos hacer el reemplazo. En este caso, el primer parámetro es la palabra que queremos reemplazar, el segundo es la que deseamos usar como sustituto. El tercer parámetro es el texto que queremos analizar, que en este caso es el contenido del post o la página.

```php

function renym_wordpress_typo_fix( $text ) {
    global $swearingWords, $nonSwearingWords;
    return str_replace($swearingWords, $nonSwearingWords, $text);
}
```

- **Función de "add_filter":**
    Esta agrega un filtro al contenido de WP utilizando la función "renym_wordpress_typo_fix" que creamos anteriormente. Esto se hace utilizando la función "add_filter" de WP, que toma dos parámetros: el primero es el nombre del filtro que queremos agregar y el segundo es la función que queremos utilizar como filtro. En este caso, el primer parámetro es "the_content" que es el nombre del filtro que queremos agregar y el segundo es la función que creamos anteriormente.

```php

add_filter( 'the_content', 'renym_wordpress_typo_fix' );
```

- **The_Content:**
  En WordPress, the_content es un gancho (hook) que se utiliza para mostrar el contenido principal de un post o página. Este gancho se emplea en el ciclo de WordPress para mostrar el contenido del post en el área de contenido de la página. Este gancho se utiliza principalmente para agregar contenido adicional antes o después del contenido del post.

