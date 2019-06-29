---
title: Creando un "port sniffer" en Rust.
layout: page
_options:
  content:
    width: 1500
    height: 2500
date: '2019-06-27 16:40:33'
categories:
- rust
- tutoriales
author_staff_member: coordinators/omar
---

> Un lenguaje de programación seguro, concurrente y práctico.

## ¿Rust?

Rust es un lenguaje de programación de sistemas introducido y apoyado por la fundación Mozilla, últimamente ha estado ganando popularidad, siendo el quinto lenguaje con mayor crecimiento según el [GitHub Octoverse](https://octoverse.github.com/projects#languages).

Según la fundación Mozilla y la [página mágica que tiene todas las respuestas)(https://wikipedia.org):

> El objetivo de Rust es ser un buen lenguaje para la creación de grandes programas del lado del cliente y del servidor que se ejecuten en Internet.

## ¿Port sniffer?

En pocas palabras un *sniffer* es una herramienta que puede interceptar datos o paquetes de datos que fluyen a través de una red.

![](https://mk0resourcesinfm536w.kinstacdn.com/wp-content/uploads/packsniffer.png)

El port sniffer que crearemos estará hecho en el lenguaje de programación Rust, no es un programa escalable y no servirá de mucho, aun así **BAJO NINGUNA CIRCUNSTANCIA** lo utilices en redes ajenas o con fines maliciosos, pues esto te puede traer problemas muy serios ☹️

El sniffer que crearemos será multihilo y podrá ser invocado desde la línea de comandos, además de poder recibir argumentos.

## Preparando el entorno

No podemos cubrir todo el lenguaje de programación Rust en un solo post, por lo tanto asumiremos que conoces las bases del lenguaje.

### Creando el proyecto con Cargo

Cargo es el gestor de paquetes de Rust y es **ASOMBROSO**. Manejará las dependencias por nosotros y nos proveerá de varias herramientas para asegurar que nuestro código sea lo mas rápido y seguro posible.

Necesitamos invocar a cargo y decirle que deseamos crear un nuevo binario, para
ello utilizaremos la orden: 

` $ cargo new ip_sniffer --bin`

Si lo hicimos correctamente Cargo creará la siguiente estructura de directorios:

```
.
├── Cargo.toml
└── src
    └── main.rs
```

Lo primero que podemos ver es un archivo llamado `Cargo.toml`, en este se
guardarán los metadatos del programa que generemos, normalmente el nombre del
creador, la fecha de creación, la versión y las dependencias necesarias para
construir el proyecto.

En el mismo nivel encontraremos un directorio llamado `src` en el cual se
encuentra un archivo `main.rs` el cual será el archivo principal ejecutado por
cargo cuando ejecutemos la orden `cargo run`.

Además de todo cargo creará dentro del directorio un nuevo repositorio de Git,
el cual puedes manejar mejor si utilizas nuestra [herramienta favorita](https://github.com).

La idea es que podamos ejecutar nuestro programa de las siguientes maneras desde
la línea de comandos:

```
ip_sniffer -h
ip_sniffer -j 100 192.168.x.x
ip_sniffer 192.168.x.x
```

## Editando `main.rs`

Toma tu editor de texto favorito (con resaltado para Rust preferiblemente) y 
comenzemos a editar el archivo `main.rs`.

El archivo inicial es así:

```rust
fn main() {
    println!("Hello World");
}
```


