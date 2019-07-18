# Joomla

## Índice de contenidos

- [Crear carpeta durante la instalación de un componente](#crear-carpeta-durante-la-instalación-de-un-componente)

## Crear carpeta durante la instalación de un componente

En script.php, importamos:

```jimport('joomla.filesystem.folder');```

Añadimos en function install($parent):

```$path = JPATH_SITE . DIRECTORY_SEPARATOR . "images" . DIRECTORY_SEPARATOR . "nombre_carpeta";
$mode = 0755;
JFolder::create($path, $mode);```

Creamos una carpeta en images para contenido multimedia.
