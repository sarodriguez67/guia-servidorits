# Como subir mi proyecto al servidor de la ITS

### Pequeña guía para que no se compliquen la vida haciendolo y les sea facil.
## Indice
- [Obtener IP del server.](#como-obtengo-la-ip-de-mi-servidor)
- [Subir archivos al server](#como-subir-archivos-a-mi-servidor)
- [Problema con los permisos - 403 Forbidden](#problemas-con-permiso-denegado)

## ¿Como obtengo la IP de mi servidor?

Esto lo verificas entrando a [servidorits.uy](https://servidorits.uy:8006) (Solo accesible mediante las computadoras de los laboratorios)

```bash
Usuario: Nombre de tu proyecto en minuscula (Ej: trinity)
Contraseña: 12345678
Realm: Proxmox VE
```

Ahi dentro dirigite a la consola de tu servidor y si te pide logearte, lo cual es muy probable, ingresá:
```bash
Usuario: uits
Contraseña: UsuarioITS
Aunque para verificar la ip no es necesario que inicies sesión (creo)
```

Deberias ver esto en la linea de comando:

```bash
uits in @TuGrupoProyecto in [Directorio]
ip: 10.0.0.xxx
>
```
Esa X son los números que faltan para iniciar de sesión.

Ya teniendo esto podemos pasar al siguiente punto.

## ¿Como subir archivos a mi servidor?
Primero deberás descargar el archivo en la PC.

<img src="https://raw.githubusercontent.com/zeusvault/uploads/main/images/8bba730b7912d35bb0c29c1565b3d5fcf353d49ffc152636228a5413cf7fdd2a.jpg" width=740>

Una vez teniendo la ip completa, ejecutá esto en la terminal de la PC.

`scp "C:\Users\its-erma03\Desktop\proyecto.zip" uits@10.0.0.x:../../var/www/html`

Con esto ya tendrias el zip subido al servidor.&nbsp;&nbsp;&nbsp;En caso probable que te haya dado  error 403 (Forbidden), [acá tenes la solución](#problemas-con-permiso-denegado)

Ahora si podemos entrar al servidor para descomprimir el zip, esto podemos hacerlo mediante la [pagina web](https://servidorits.uy:8006) o mdiante SSH. Para acceder desde SSH hay que seguir el proceso que se explica en [este punto](#
Ahora debemos acceder a la ruta a donde subimos el archivo para poder descomprimirlo.
```bash
cd /var/www/html
```
Y una vez dentro, descomprimimos con `unzip proyecto.zip`

### Recomendación del profesor Joaquín Perez
Cada vez que se quiera actualizar el proyecto, [se deberá realizar un nuevo zip y subirlo.](#como-subir-archivos-a-mi-servidor)
Para subir el proyecto nuevamente sin problemas, eliminamos la carpeta entera:
```bash
cd /var/www/html
sudo rm -r carpetaProyecto
```

# Problemas con permiso denegado
Ejecuta el siguiente comando:
`ssh uits@10.0.0.X`

E iniciaremos sesión con las credenciales vistas previamente:
```bash
Usuario: uits
Contraseña: UsuarioITS
```

Con esto te conectarás al servidor como si estuvieras dentro de la [web](https://servidorits.uy:8006)

### ¿Que haremos con esto?

Le daremos permiso de escritura al directorio donde dejaremos el repositorio.

Ejecutaremos:

```bash
cd /var/www/html
sudo chmod o+w /var/www/html
```
Para comprobar ejecutamos `ls -l ..`. Los ultimos 3 permisos deben tener una w (`drwxr-xrwx.`)

Con esto ya podemos usar [scp](#como-subir-archivos-a-mi-servidor) para subir los archivos.

##

> Ya de paso seguime en mi [cuenta principal](https://github.com/Smokyy14) , ¿no?
