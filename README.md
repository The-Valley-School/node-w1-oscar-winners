# Workshop 1 - API de Ganadores de los Oscar

En este WorkShop debemos llevar a cabo un API de ganadores de los premios Oscar:

![Untitled](/assets/Untitled.png)

Para ello debes hacer uso de express y lectura/escritura de ficheros.

Como puedes observar existen varios endpoints:

**GET / (home)**

Nos devolverá el HTML que ves en la captura. Este HTML servirá a modo de documentación, ya que nos indicará todos los endpoints que existen.

**GET /oscars**

Esto nos devolverá los años disponibles para consultar los oscar:

![Untitled](/assets/Untitled%201.png)

Para sacar la lista de años disponibles deberás leer la carpeta donde tengas todos los ficheros json con los oscar y ver qué años tenemos disponibles:

![Untitled](/assets/Untitled%202.png)

Para recorrrer los ficheros de una carpeta puedes usar la función fs.readdir, que te devolverá un array con el nombre de los ficheros que contiene esa carpeta:

<https://nodejs.org/api/fs.html#fsreaddirpath-options-callback>

**GET /oscars/{oscar_year}**

Este endpoint buscará el fichero correspondiente a ese año y lo devolverá en formato JSON

Si ese año no está contemplado dentro de la carpeta data, deberá devolver 404

![Untitled](/assets/Untitled%203.png)

**POST /oscars/{oscar_year}**

Este endpoint permitirá añadir un premio a un año concreto, para probarlo puedes hacer uso de fetch y chrome:

```jsx
const oscar = {
  category: "Invented Category",
  entity: "Fran Linde",
};

fetch("http://localhost:3000/oscars/2019", {
  body: JSON.stringify(oscar),
  method: "POST",
  headers: {
    Accept: "application/json",
    "Content-Type": "application/json",
  },
}).then((data) => console.log(data));
```

En caso de existir el JSON correspondiente lo añadirá al final.

Si no existiera el JSON deberá crearlo y añadir este premio.

**GET /winners-multiple/{oscar_year}**

Este endpoint devolverá un objeto con aquellos premiados que hayan recibido más de un Oscar, por ejemplo en 2012.

<http://localhost:3000/winners-multiple/2012>

![Untitled](/assets/Untitled%204.png)

Devolverá un JSON como este:

```jsx
{
  "winners": [
    {
      "name": "Life of Pi",
      "awards": [
        {
          "category": "CINEMATOGRAPHY",
          "year": "2012"
        },
        {
          "category": "DIRECTING",
          "year": "2012"
        },
        {
          "category": "MUSIC (Original Score)",
          "year": "2012"
        },
        {
          "category": "VISUAL EFFECTS",
          "year": "2012"
        }
      ]
    },
    {
      "name": "Argo",
      "awards": [
        {
          "category": "FILM EDITING",
          "year": "2012"
        },
        {
          "category": "BEST PICTURE",
          "year": "2012"
        },
        {
          "category": "WRITING (Adapted Screenplay)",
          "year": "2012"
        }
      ]
    },
    {
      "name": "Les Misérables",
      "awards": [
        {
          "category": "MAKEUP AND HAIRSTYLING",
          "year": "2012"
        },
        {
          "category": "SOUND MIXING",
          "year": "2012"
        }
      ]
    },
    {
      "name": "Skyfall",
      "awards": [
        {
          "category": "MUSIC (Original Song)",
          "year": "2012"
        },
        {
          "category": "SOUND EDITING",
          "year": "2012"
        }
      ]
    }
  ]
}
```

Aquí podrás encontrar los JSONs de los Oscar:

<https://github.com/The-Valley-School/node-w1-oscar-winners/tree/main/data>
