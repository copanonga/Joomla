# Joomla

## Índice de contenidos

- [Crear carpeta durante la instalación de un componente](#crear-carpeta-durante-la-instalación-de-un-componente)
- [Fecha](#fecha)
- [Insertar en base de datos](#insertar-en-base-de-datos)

## Crear carpeta durante la instalación de un componente

En script.php, importamos:

```
jimport('joomla.filesystem.folder');
```

Añadimos en function install($parent):

```
$path = JPATH_SITE . DIRECTORY_SEPARATOR . "images" . DIRECTORY_SEPARATOR . "nombre_carpeta";
$mode = 0755;
JFolder::create($path, $mode);
```

Creamos una carpeta en images para contenido multimedia.

## Fecha

```
$config  = JFactory::getConfig();
$offset  = $config->get('offset');    
$fecha   = JFactory::getDate('now', $offset);
```

## Insertar en base de datos

```
$db = JFactory::getDbo();

$insertarDato = new stdClass();
$insertarDato->dato001  = 'Dato 001';
$insertarDato->dato002   = 'Dato 002';
$result = $db->insertObject('#__tabla', $insertarDato);

$nuevoId = $db->insertid();
```
