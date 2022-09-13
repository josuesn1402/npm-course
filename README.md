# Gestión de Dependencias y Paquetes con NPM
Link al curso: [Curso de Gestión de Dependencias y Paquetes con NPM](https://platzi.com/cursos/npm-js/)

## Archivo de configuración package.json
El archivo package.json es un archivo de configuración que contiene la información más importante de tu proyecto como: datos específicos, dependencias, dependencias de desarrollo y archivos de ejecución.

El archivo `package.json` estaría estructurado inicialmente por las siguientes propiedades:

`name`:			nombre del proyecto.
`version`:		versión del proyecto.
`description`:	breve descripción sobre el proyecto.
`main`:			archivo principal del proyecto.
`scripts`:		comandos de ejecución del proyecto.
`keywords`:		palabras clave del proyecto.
`author`:		nombre y correo electrónico del creato/propietario del proyecto.
`license`:		licencia del proyecto.

## Inicialización del `package.json`

$ `npm init`:	 Genera de manual el package, pidiendo los valores para la información de nuestro proyecto.
$ `npm init -y`: Autogenera el archivo con las configuaraciones mínimas.

### Declaración de valores por defecto
$ `npm set init.author.email <email>`:	 Establece nombre por defecto del autor
$ `npm set init.author.name <name>`:	 Establece correo electrónico por defecto del autor
$ `npm set init.license <license name>`: Establece licencia por defecto que tendran los proyectos

> Al ejecutar `npm init -y` el archivo se creará con los valores que se le preestableca.