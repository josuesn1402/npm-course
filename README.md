# Gestión de Dependencias y Paquetes con NPM
Link al curso: [Curso de Gestión de Dependencias y Paquetes con NPM](https://platzi.com/cursos/npm-js/)

## Archivo de configuración package.json
El archivo package.json es un archivo de configuración que contiene la información más importante de tu proyecto como: datos específicos, dependencias, dependencias de desarrollo y archivos de ejecución.

El archivo `package.json` estaría estructurado inicialmente por las siguientes propiedades:

* **name**:		 	nombre del proyecto.
* **version**:	 	versión del proyecto.
* **description**:	breve descripción sobre el proyecto.
* **main**:		 	archivo principal del proyecto.
* **scripts**:	 	comandos de ejecución del proyecto.
* **keywords**:	 	palabras clave del proyecto.
* **author**:		nombre y correo electrónico del creato/propietario del proyecto.
* **license**:	 	licencia del proyecto.



## Inicialización del package.json

$ `npm init`:	Genera de manual el package, pidiendo los valores para la información de nuestro proyecto.

$ `npm init -y`: Autogenera el archivo con las configuaraciones mínimas.


### Declaración de valores por defecto
$ `npm set init.author.email <email>`: Establece nombre por defecto del autor

$ `npm set init.author.name <name>`: Establece correo electrónico por defecto del autor

$ `npm set init.license <license name>`: Establece licencia por defecto que tendran los proyectos


> Al ejecutar `npm init -y` el archivo se creará con los valores que se le preestableca.



## Instalación de dependencias
Las dependencias y paquetes son recursos que vamos a utilizar en nuestro proyecto, el conjunto de módulos para resolver un problema mayor.

Estás deben instalarse en la carpeta raíz del proyecto.

> 💡 Más información sobre `npm install`: https://docs.npmjs.com/cli/v8/commands/npm-install


$ `npm i <pkg>` | `npm install <pkg>` | `npm install <pkg> --save` | `npm install <pkg> -S`:

Instala un paquete, por defecto se instalara como dependecia requeridas para el funcionamiento del proyecto, por lo que no es necesario colocar `--save`. Colocar `i` o `install` es lo mismo, al igual que `--save` y `-S`.

$ `npm install <pkg> --save-dev` | `npm install <pkg> -D`:

Instala los paquetes como dependecias de desarrollo, que no serán pasadas a producción.

$ `npm install <pkg> -O`:

Con este comando podemos instalar de manera opcional un paquete.

$ `npm install --save-exact <pkg>` | `npm i -E <pkg>`:

Instala nuestras dependencias a utilizar con una versión exacta.

$ `npm install <pkg> -g`:

Instala globalmente un paquete, puede ser instalado en diferentes proyectos. Puede que puda permisos de administrador.

> 💡 Evitar que solicite permisos de administrador https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally

$ `npm list`: Lista los paquetes del proyecto.

$ `npm list -g --depth 0`:
Lista los paquetes instalos globalmente

> 💡 La dependencia `nodemon` instala un 'Demonio' (Un servicio que corre en segundo plano en el sistema), este se encargará de detectar los cambios que hagamos en un archivo y actualizar el puerto en `localhost` automaticamente

$ `npm install --force <pkg>` | `npm install -f <pkg>`:

Instala el paquete de manera forzada y fuerza a que sea el último recurso o versión desde el servidor de NPM.

$ `npm install <pkg> --dry-run`:

Simula la instalación de una dependencia, mostrandonos su output como si estuviese intalandolo, pero sin hacerlo.

$ `npm install <pkg>@<version>`:

Instala una versión en específico de un paquete.


### Instalar dependencias a partir de `package.json`
Tan solo escribes `npm install` o `npm i` y se instalarán según el contenido del archivo, pero las versiones instaladas pueden cambiar si tiene el carácter 'caret' =  `^`:

* Usando **caret**:

	```json
	{
	  "dependencies": {
	    "moment": "^2.29.4"
	  },
	  "devDependencies": {
	    "date-fns": "^2.29.2",
	    "nodemon": "^2.0.19",
	    "webpack": "^5.74.0"
	  },
	  "optionalDependencies": {
	    "eslint": "^8.23.1"
	  }
	}
	```

	El caret hace referencia a que los paquetes se instalarán a una versión más reciente, esto puede romper el funcionamiento del proyecto. Por ejemplo, si alguién clona un repositorio y quiere instalar las dependencias del proyecto, puede que obtenga errores al tener paquetes con versiones diferentes de las que se uso para crear el proyecto.

* Sin usar **caret**:

	```json
	{
	  "dependencies": {
	    "moment": "2.29.4"
	  },
	  "devDependencies": {
	    "date-fns": "2.29.2",
	    "nodemon": "2.0.19",
	    "webpack": "5.74.0"
	  },
	  "optionalDependencies": {
	    "eslint": "8.23.1"
	  }
	}
	```

	Al quitar el caret, se instalarán las mismas versiones que se ven en el archivo `package`, así  que el proyecto funcionará de igual manera para quién lo haga y para otra persona que también lo utilice.



## Actualizar paquetes
$ `npm outdate`:	 	Mostrará los paquetes que están desactualizados y las ultimás versiones disponibles.

$ `npm outdate --dd`:	Para ver un output más detallado.

$ `npm update`:		 	Actualizar los paquetes que no están en la ultima versión.

$ `npm install <pkg>@latest`: Actualizar un paquete especifico



## Eliminar paquetes
$ `npm uninstall <pkg>`:	Eliminando el paquete del `package.json` y del directorio `node_modules`.

$ `npm uninstall <pkg> --no-save`: Eliminando **solamente** del directorio `node_modules`.



## Archivo package-lock.json
El archivo `package-lock.json` describe todo el árbol de dependencias de cada paquete instalado. Cuando alguien hace fork de un repositorio no tiene el directorio node_modules.



## Uso los símbolos para el versionado de paquetes
El versionado de paquetes está conformado por tres valores:

* **Major**: el valor que muestra la versión que contiene los cambios importantes del paquete
* **Minor**: el valor que muestra la versión que contiene los cambios en funcionalidades, pero no representan un cambio significativo
* **Patch**: el valor que muestra la versión que contiene cambios rápidos para solucionar problemas de seguridad o bugs

	![Versionado de paquetes](https://static.platzi.com/media/user_upload/wheelbarrel-no-tilde-caret-white-bg-w1000-72ca1a72-4c7f-4abe-8482-425c01a72f89.jpg)


### Símbolos ^ y ~ para actualizar las versiones minor y patch
Existen dos símbolos que acompañan a este versionado, que sirven para actualizar las versiones _minor_ y _patch_ del paquete:

* `Caret (^)`: Permite actualizar las versiones _minor_ y _patch_
* `Tilde (~)`: Permite actualizar las versiones _patch_


### Otros símbolos:
* `<`	: Versión menor a la indicada.
* `<=`  : Versión menor o igual a la indicada.
* `>`	: Versión mayor a la indicada.
* `>=`  : Versión mayor o igual a la indicada.

```json
"dependencies": {
    "json-server": ">0.15.1",
    "moment": ">=2.26.0",
    "date-fns": "<2.14.0",
    "express": "<=4.17.3"
}
```


## Apartado de "scripts" en package.json
Indica los comandos a ejecutar del proyecto.

### Crear comando
Los comandos se crean con la siguiente estructura dentro del `package.json`:

```json
{
    "scripts": {
        "<name>": "<comand>"
    }
}
```
* **name**	: Nombre del comando (tiene que ser descriptivo).
* **comand**  : Comando que se ejecutarpar en la terminal.

Se ejecutan usando `npm run <script-name>`.

```json
{
    "scripts": {
		"dev": "webpack-dev-server --mode development",
		"build": "webpack --mode production",
		"start": "serve ./dist -s -l 8080"
    }
}
```
* **dev**  : Modo desarrollo.
* **build**: Compila todo y me crea un directorio dist.
* **start**: Toma el directorio dist y lanzo un servidor en modo producción.

[Fuente](https://platzi.com/comentario/883390/)

```bash
$ npm run start
$ npm run build
$ npm run deploy
```

### Scripts con "pre" y "post" 
Al especificar "pre" en un script, este se ejecutará automáticamente antes del comando que ejecutaste. 
Por ejemplo, si defines el comando `build` y `prebuild`, cuando corras `npm run build` el comando `prebuild` se ejecutará primero.
Esto sirbe para poder ejecutar tareas que hagan algún tipo de preparación necesaria para correr el comando principal. Sin embargo, hay que hacer notar que si el comando pre falla (retorna un valor que no es 0) el comando principal no se ejecutará. Esto es algo bueno ya que si nuestro proceso de preparación no se realiza de forma exitosa, puede que tengamos problemas al querer ejecutar la tarea principal.

En algunas ocaciones, sin embargo, la tarea previa puede fallar sin que eso afecte la ejecución de la tarea principal. En esos casos puedes usar `|| exit 0` para retornar 0:

```json
	"presass-build": "(rm css/*.css; rm css/*.css.map) || exit 0"
```

En este, `rm` puede fallar si el directorio **css** está vacio, y en ese caso no hay problema, la tarea principal puede funcionar sin ningún problema ya que `presass-build` tiene el propósito de vaciar ese directorio.


Video de referencia sobre "post": https://www.youtube.com/watch?v=kwn7tHJJoLA

[Fuente](https://platzi.com/comentario/885229/)


### Listar scripts
También es posible utilizar el comando `ntl` (npm task list) para utilizar un menú de texto y seleccionar la tarea de una forma más interactiva. 
Para ello, sólo tenemos que escribir `npx ntl`

[Fuente](https://lenguajejs.com/npm/administracion/scripts-de-npm/)


> NOTA: para problemas de webkpack al ejecutar `build` o `start`:  
>* Revisar este repo: https://github.com/webpack/webpack/issues/14532  
>* O probar este comando: `export NODE_OPTIONS=--openssl-legacy-provider`



## Solución de problemas
Alguno de los errores que pueden ocurrir son:

* Errores en la configuración del archivo `package.json`
* Errores del sistema operativo
* Configuración errónea de Git o GitHub
* Errores ortográficos (typos)
* O errores que no estén ligados directamente a NPM


### Mostrar detalles del comando ejecutado
Para identificar el error que puede existir en tu proyecto, es necesario analizar cada paso que ejecuta un comando, para saber qué o en dónde ocurre el problema.

El flag `--dd` en un comando de NPM, te mostrará de manera verbosa cada paso que se ejecuta. De esta manera podrás observar si existe un error para solucionarlo.

```bash
npm [comand] --dd
```

Para poder activar la opción de verbose (es decir que nos muestre mayor información de lo que esta haciendo el comando)

```bash
npm run [comando] --dd
```

[Fuente](https://platzi.com/comentario/1188608/)


Otra forma, es ejecutar el comando de NPM. Si existe un error, la terminal te mostrará los diferentes errores que encontró. Al final de este resumen, existirá una ruta con los detalles del error, lo puedes abrir para observar los pasos que ejecutó NPM.

![Error](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/npm03.PNG)


### Error en node_modules
Uno de los problemas que podemos toparnos, es que nuestros archivos de `node_moduls` no estén correctamente instalados o tengamos una versión anterior.

$ `npm cache clean -f` | `npm cache clean --force`: Borra el cache de npm.

$ `npm cache verify`: Muestra la cantidad de cache existente, podemos cercioraros de si ya fue eliminado.

$ `npm ci`: es como hacer `rm -rf node_modules` y `npm i` en un solo paso, lo que haces es un `clean install` o `instalacion limpia`. 
[Fuente](https://platzi.com/comentario/2223998/) - [Documentación](https://docs.npmjs.com/cli/v8/commands/npm-ci)


#### Paquetes que podemos usar para elimar node_modules de manera más segura
* [rimraf](https://github.com/isaacs/rimraf)
* [npkill](https://github.com/voidcosmos/npkill)









