# Joomla

## Índice de contenidos

- [Crear carpeta durante la instalación de un componente](#crear-carpeta-durante-la-instalación-de-un-componente)
- [Fecha](#fecha)
- [Insertar en base de datos](#insertar-en-base-de-datos)
- [Enviar correo](#enviar-correo)
- [Select](#select)
- [Mostrar popover en modal](#mostrar-popover-en-modal)

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

## Enviar correo

```
$subject = "Asunto";
        
$body .= 'Texto';

$from = array("info@correo.es", "Info");
$to = "hola@correo.es";

$mailer = JFactory::getMailer();
$mailer->setSender($from);

$mailer->addRecipient($to);

$correosAEnviar = array();
array_push($correosAEnviar, "hola@demo.es");

foreach ($correosAEnviar as $correo) {
    $mailer->addBCC($correo);
}

$mailer->setSubject($subject);
$mailer->setBody($body);
$mailer->isHTML();

$isSend = $mailer->send(); 

if ($isSend==0) {
    return 'Error sending email';
} else {
    return "Enviado";
}
```

## Select

```
$db = JFactory::getDbo(); 
        
$query	= $db->getQuery(true);
$query->select(array('u.data'));
$query->from(('#__datos').' AS u');
$query->join('LEFT', $db->quoteName('#__datos001', 'a') . ' ON (' . $db->quoteName('u.id') . ' = ' . $db->quoteName('a.id') . ')');
$query->where('(u.numero = '.$datoABuscar.')');
$query->where('(u.estado = 1)');
$query->order('u.ordering ASC');

$db->setQuery($query);
$result = $db->loadObjectlist();
```

## Mostrar popover en modal

```
$document  = JFactory::getDocument();
$popover      = '.popover {z-index: 99999;}';
$document->addStyleDeclaration($popover);

<p      
        data-toggle="popover"
        data-placement="top"
        data-trigger="hover"
        data-original-title="Título"
        data-content="Contenido">
        Día completo
</p>

<script>
    
    $(document).ready(function(){
        $('[data-toggle="popover"]').popover();
    });
    
</script>    
```
