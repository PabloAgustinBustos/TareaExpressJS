# Construcción de una API REST

> Repaso rápido. Una **API REST** a sencillas formas es **una máquina que te da los datos que vos le pidas**. Si le pedis todos los empleados de una empresa con todos sus datos, te los da. Si le pedis que en lugar de todos los empleados, solo queres 6, te los da. Si los queres ordenados alfabeticamente, te los da. Si queres **solamente** los empleados que tienen 10 años de experiencia, ordenados de menor a mayor, segun los lenguajes y tecnologías que manejan, te lo da.
> Esa máquina es un intermediario (interfaz) entre el cliente y la base de datos. El cliente no sabe pedirle datos a la base de datos porque por así decirlo, los dos hablan idiomas diferentes (por ejemplo, el cliente habla italiano y la base de datos habla griego) y necesitan de un intermediario que traduzca (la API REST)

## 1- Preparando la "base de datos"

> Como **no se manejará una base de datos real** con mysql o postgreSQL o SQLite, se manejará una especie de pseudo-base de datos que es simplemente un archivo .json que contiene los datos.

Lo primero es ir al archivo llamado `data.json` que está en la carpeta db.
Lo que contiene es un array de 3 videojuegos (un array de objetos).
Hay que agregarle 27 juegos más para que sumen en total 30. También hay que buscar 4 imágenes de los juegos que se agreguen

Los videojuegos contienen los siguientes datos:

 - title: String
 - developer: Strings
 - publisher:  Strings
 - genres: Array de strings
 - release: Objeto con siguiente estructura:
	 - day: Number
	 - month: Number
	 - year: Number
 - plataforms: Array de objetos con siguiente estructura:
	 - name: String
	 - releaseDate: Objeto con siguiente estructura:
		 - day: Number
		 - month: Number
		 - year: Number
 - engine: String
 - modes: Objeto con siguiente estructura
	 - single-player: bool
	 - multiplayer: bool
 - images: Array de strings
 - premise: String

> -El atributo release contiene la fecha principal (hay que tener en cuenta que pueden variar las fechas de lanzamiento según las plataformas)
> 
> -platforms es un array de objetos, cáda objeto representa una plataforma que puede ser ps4, xbox360, etc. La info de cáda objeto justamente es el nombre de la plataforma y la fecha de lanzamiento para esa plataforma (devuelta un objeto)
> 
> -images es un array de strings, los strings son url donde están ubicadas las imágenes

Ejemplo: 

    [
		{

			"title": "Elden Ring",
			"developer": "FromSoftware",
			"publisher": "Bandai Namco Entertainment",
			"genres": ["arpg"],
			
			"release": {
				"day": 25,
				"month": 2,
				"year": 2022
			},

			"platforms":  [
				{
					"name":  "Xbox One",
					"releaseDate":  {
						"day":  25,
						"month":  2,
						"year":  2022
					}
				},
				
				{
					"name":  "Xbox Series X/S",
					"releaseDate":  {
						"day":  25,
						"month":  2,
						"year":  2022
					}
				},
			
				{
					"name":  "PlayStation 4",
					"releaseDate":  {
						"day":  25,
						"month":  2,
						"year":  2022
					}
				},
				
				{
					"name":  "PlayStation 5",
					"releaseDate":  {
						"day":  25,
						"month":  2,
						"year":  2022
					}
				},
	
				{
					"name":  "Pc",
					"releaseDate":  {
						"day":  25,
						"month":  2,
						"year":  2022
					}
				}
			],

			"engine":  "unknown",
			
			"modes":  {
				"single-player":  true,
				"multiplayer":  true
			},
			
			"images":  [
				"db/images/EldenRing/1.jpg",
				"db/images/EldenRing/2.png",
				"db/images/EldenRing/3.png",
				"db/images/EldenRing/4.png"
			],
			
			"premise":  "Elden Ring takes place in the Lands Between, an island populated by a number of gods. The Elden Ring was created by a god called the Greater Will, who hurled it down from the cosmos in an attempt to bring order to the world. The Ring was housed inside the Erdtree, a golden tree that acts as a symbol of the Greater Will. The Lands Between were ruled over by Queen Marika the Eternal, who acted as keeper of the Elden Ring and had numerous children. Marika eventually shattered the Elden Ring into multiple pieces and disappeared, causing her demigod children to war over pieces of the Ring in an event called the Shattering. Each demigod possesses a shard of the Ring, collectively called the Great Runes, which corrupt them with power. The player character is a Tarnished, one of a group of exiles from the Lands Between who were summoned back after the Shattering. As one of the Tarnished, the player must traverse the realm to become the Elden Lord"
		},

		{
			"title":  "Grand Theft Auto V",
			"developer":  "Rockstar North",
			"publisher":  "Rockstar Games",
			"genres":  ["action",  "adventure",  "open-world"],
			
			"release":  {
				"day":  17,
				"month":  9,
				"year":  2013
			},

			"platforms":  [
				{
					"name":  "Xbox 360",
					"releaseDate":  {
						"day":  17,
						"month":  9,
						"year":  2013
					}
				},
				
				{
					"name":  "Xbox One",
					"releaseDate":  {
						"day":  18,
						"month":  11,
						"year":  2014
					}
				},
				
				{
					"name":  "Xbox Series X/S",
					"releaseDate":  {
						"day":  15,
						"month":  3,
						"year":  2022
					}
				},
				
				{
					"name":  "Playstation 3",
					"releaseDate":  {
						"day":  17,
						"month":  9,
						"year":  2013
					}
				},
				
				{
					"name":  "PlayStation 4",
					"releaseDate":  {
						"day":  18,
						"month":  11,
						"year":  2014
					}
				},
				
				{
					"name":  "PlayStation 5",
					"releaseDate":  {
						"day":  15,
						"month":  3,
						"year":  2022
					}
				},
				
				{
					"name":  "Pc",
					"releaseDate":  {
						"day":  14,
						"month":  4,
						"year":  2015
					}
				}
			],

			"engine":  "RAGE",
			
			"modes":  {
				"single-player":  true,
				"multiplayer":  true
			},

			"images":  [
				"db/images/GrandTheftAutoV/1.jpg",
				"db/images/GrandTheftAutoV/2.jpg",
				"db/images/GrandTheftAutoV/3.jpg",
				"db/images/GrandTheftAutoV/4.jpg"
			],
			
			"premise":  "When a young street hustler, a retired bank robber and a terrifying psychopath find themselves entangled with some of the most frightening and deranged elements of the criminal underworld, the U.S. government and the entertainment industry, they must pull off a series of dangerous heists to survive in a ruthless city in which they can trust nobody, least of all each other."
		},

		{
			"title":  "Assasin's Creed",
			"developer":  "Ubisoft Montreal",
			"publisher":  "Ubisoft",
			"genres":  ["action",  "adventure",  "stealth"],
			
			"release":  {
				"day":  13,
				"month":  11,
				"year":  2007
			},
			
			"platforms":  [
				{
					"name":  "Xbox 360",
					"releaseDate":  {
						"day":  13,
						"month":  11,
						"year":  2007
					}
				},
				
				{
					"name":  "Playstation 3",
					"releaseDate":  {
						"day":  13,
						"month":  11,
						"year":  2007
					}
				
				},

				{
					"name":  "Pc",
					"releaseDate":  {
						"day":  8,
						"month":  4,
						"year":  2008
					}
				}
			],
			
			"engine":  "Ubisoft Anvil",
			
			"modes":  {
				"single-player":  true,
				"multiplayer":  false
			},
			
			"images":  [
				"db/images/AssassinsCreed/1.jpg",
				"db/images/AssassinsCreed/2.jpg",
				"db/images/AssassinsCreed/3.jpg",
				"db/images/AssassinsCreed/4.jpg"
			],
			
			"premise":  "Desmond Miles, a bartender, is kidnapped by the company Abstergo Industries for use as a test subject in the 'Animus', a device that can simulate genetic memory. Abstergo intends to put Desmond in the device to recall the memories of his ancestor, Altaïr Ibn-La'Ahad, a member of the Assassin Brotherhood in the year 1191, who lived during the Third Crusade in the Holy Land. Initially, Desmond has trouble adjusting to the device, but eventually relives Altaïr's exploits over the next several days. The game then primarily changes to Altaïr's point-of-view, with occasional transitions to Desmond, due to problems with the Animus or onset of the Bleeding."
		}	    
    ]

## 2- Preparando funciones
La idea es tener dos archivos, uno llamado `filterFunctions.js` y otro llamado `orderFunctions.js`. Lo que tienen son **definiciones de funciones** que servirán para recibir los datos y **filtrarlos** u **ordenarlos**.
Estos archivos lo que deben hacer es **primero leer el archivo `data.json`**  y luego de tener escritas las definiciones de las funciones deben **exportar esas funciones**, para que luego otro archivo `index.js` pueda hacer uso de esas funciones.

> El archivo index.js va a importar las funciones de los dos archivos. Este archivo index.js será la API REST que contendrá las rutas de back-end.
> 
> Lo ideal sería trabajar con un lenguaje de bases de datos para obtener los datos ordenados y/o filtrados, pero la idea de esta tarea es trabajar peticiones GET con Express, sin tocar SQL.

Las funciones son:
|Función|Lo que hace|
|--|--|
| `getGames([number]): Array` | te retorna un array con todos los juegos, simplemente eso. |
| `getGamesByGenre(genre, [games]): Array | bool` | te retorna un array de juegos pero solamente con los juegos que sean del género indicado como argumento. Si no encuentra juegos de ese género, retorna un `false`. Contiene un parámetro opcional llamado `games` En el que, si se le manda un array de juegos como argumento, tiene que retornar los juegos del género indicado pero del array que se le manda por argumento. Si no recibe ningún array, usará el array de juegos que agarra del `.json`.
 | `getGamesByDev(devName, [games]): Array | bool` | retorna un array con los juegos que desarrolló la empresa indicada como argumento. Si no encuentra ningún juego, retorna `false`. También tiene un parámetro opcional que sigue lo mismo que la función anterior. Si se le manda un array, filtrará el array mandado como argumento, sino entonces usará el array del `.json`.
 | `getGamesByPlatform(platform, [games]): Array | bool` | Me filtra los juegos según la plataforma. Si quiero los juegos de playstation 5, le mando eso como argumento en platform y me retornará el array de juegos de esa plataforma. Igual que los anteriores, si le mando un array `games`, me filtrará ese array, sino, usará el array completo del `.json`.
 |`getGamesByDate([min], [max], [games]): Array | String | bool`| La idea es que me retorne los juegos que salieron entre una fecha y otra. Le mando la primer fecha (min) y la segunda fecha (max) y ambos son strings con la estructura `"dd-mm-yyyy"`. Si por ejemplo, le mando `min` pero no le mando `max`, lo que hace es retornarme los juegos que salieron desde la fecha `min` **hasta ahora** (Osea, los juegos cuyas fechas de `release` son mayores a `min`). Si le mando `max` pero no le mando `min`, entonces retorna los juegos cuyas fechas de `release` sean menores a `max`. Si le mando los dos argumentos (min y max) entonces debe **verificar que la fecha `min` sea menor a la fecha `max`** y luego de eso los filtra. Si no se cumple esa condición, retorna un string que diga "ERROR: La primer fecha es mayor a la segunda fecha". Ahora si le mando bien las fechas, pero no encuentra ningún juego lanzado entre esas fechas, retorna un false. Devuelta yo le puedo mandar un array para que filtre ese array, o usar el del .json si no se lo mando.
 |`orderByTitle(games): Array` | Le mando un array de juegos, me los ordena alfabéticamente según el título del juego y por último me lo retorna.
 |`orderByDate(games): Array`|Lo mismo, me retorna el array ordenado según la fecha de salida de cada juego (usar el atributo release).

Por último, probar las funciones haciendo testing.
Hay que probar los siguientes casos:

## 3- Armando la API REST
Ahora que ya tenemos la "base de datos" con las funciones, lo próximo es crear un archivo `index.js` que importará las funciones de los dos archivos.
Luego de importarlas se comienza con la estructura básica de Express y se definen los endpoints a los cuales se les harán peticiones GET.
Rutas:

 - `/` -> Lo que hace es dar un json con el atributo link y el siguiente endpoint
 - `/games?number&minDate&maxDate&order` -> Si no se le manda query-strings, devuelve un json con todos los juegos en la "base de datos". Ahora si se le manda los query-string, debe ordenar el array o filtrarlo, dependiendo de qué se le mande.
 
	 Ejemplo:
	 - hago petición GET a `/games` me da un json con **todos** los juegos
	 - hago petición GET a `/games?order=title` me da un json con todos los juegos pero **ordenados** alfabéticamente según el **título**
	 - hago petición GET a `/games?number=4&minDate=13-11-2007&maxDate20-12-2007&order=title` me da un json con 4 juegos que fueron lanzados desde el 13/11/2007 hasta el 20/12/2007 y ordenados alfabéticamente según el **título**
	 - hago petición GET a `/games?minDate=1-1-2015` Me da un json con todos los juegos que fueron lanzados desde principios del 2015 hasta hoy
	 - hago petición GET a `/games?maxDate=24-10-2005&order=date` me da todos los juegos que fueron lanzados hasta el 24/10/2005 ordenados de menor a mayor según la fecha de release.
 - `/games/:platform?number&minDate&maxDate&order` -> me da los juegos de una plataforma específica
- `/games/:genre?number&minDate&maxDate&order`
 - `/games/:developer?number&minDate&maxDate&order` -> me da los juegos de una desarrolladora de videojuegos
 - `/games/:developer/:platform?number&minDate&maxDate&order` -> me da los juegos que desarrolló una desarrolladora para una plataforma indicada.

## 4- Armar un front-end (opcional)
La idea es tener una página index.html, donde muestre una tabla con información de todos los juegos. (mostrar las imágenes de la carpeta images)
Ejemplo:

<table>
        <tr>
            <th>id</th>
            <th></th>
            <th>title</th><th></th>
            <th>developer</th><th></th>
            <th>publisher</th><th></th>
            <th>genres</th><th></th>
            <th>release</th><th></th>
            <th>platforms</th><th></th>
            <th>engine</th><th></th>
            <th>modes</th><th></th>
            <th>images</th><th></th>
            <th>premise</th>
        </tr>
        <tr>
            <td>1</td><td></td>
            <td>Elden Ring</td><td></td>
            <td>FromSoftware</td><td></td>
            <td>Bandai Namco Entertainment</td><td></td>
            <td>arpg</td><td></td>
            <td>25/2/2022</td><td></td>
            <td>Xbox One, Xbox Series X/S, Playstation 4, Playstation 5, Pc</td><td></td>
            <td>unknown</td><td></td>
            <td>single-player and multiplayer</td><td></td>
            <td>imagenes</td><td></td>
            <td>Elden Ring takes place in blablabla</td>
        </tr>
        <tr>
            <td>2</td><td></td>
            <td>Grand Theft Auto V</td><td></td>
            <td>Rockstar North</td><td></td>
            <td>Rockstar Games</td><td></td>
            <td>action, adventure, open-world</td><td></td>
            <td>17/9/2013</td><td></td>
            <td>Xbox 360, Xbox One, Xbox Series X/S, Playstation 3 Playstation 4, Playstation 5, Pc</td><td></td>
            <td>RAGE</td><td></td>
            <td>single-player and multiplayer</td><td></td>
            <td>imagenes</td><td></td>
            <td>When a young street hustler, a retired bank robber and a terrifying psychopath find themselves entangled with some bla bla bla</td>
        </tr>
        <tr>
            <td>3</td><td></td>
            <td>Assassin's Creed</td><td></td>
            <td>Ubisoft Montreal</td><td></td>
            <td>Ubisoft</td><td></td>
            <td>action, adventure, stealth</td><td></td>
            <td>13/11/2007</td><td></td>
            <td>Xbox 360, Playstation 3, Pc</td><td></td>
            <td>Ubisoft Anvil</td><td></td>
            <td>single-player</td><td></td>
            <td>imagenes</td><td></td>
            <td>Desmond Miles, a bartender, is kidnapped by bla bla bla</td>
        </tr>
</table>

También debe tener inputs que sirvan para filtrar y ordenar la tabla.

 - Un input number que sirva para indicar la cantidad de juegos que queremos (si está en cero, se trae todos los juegos)
 - Otro input de tipo text donde se le indique de qué empresa queremos los juegos (Si está vacío, se traerá de todas empresa)
 - Otro input de tipo text donde se le indique el género (Si está vacío, trae de todos los géneros)
 - Dos inputs de tipos date, en uno se indica la fecha min y en el otro se indica la fecha max
 - un select con tres options (default, title y date) que sirva para indicar si ordenarlos según el título o según la fecha de release. Si está en default, los trae como estan en la base de datos.

También debe haber un botón que diga "buscar" en el que haga la petición al endpoint correspondiente según los inputs.
