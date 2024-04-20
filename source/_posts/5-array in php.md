---
title: array in php
subtitle: array in php
categories:
    - personal
---
![me.jpg](/assets/img/php-logo.png)

Php (pre-processore di ipertesti), è un linguaggio di scripting interpretato concepito principalmente per la programmazione web lato server. <br>
In questa piccola lezione vedremo come si dichiara un array e successivamente come ciclarlo. <br>

1. **dichiarazione di un array di stringhe in php**

```php
<?php
    $array = ["Luca", "Mario", "Dario", "Andrea"];
?>
```

2. **ciclare l'array di stringhe**

```php
<?php
    for ($i = 0; $i < count($array); $i++){
        echo $array;
    }
?>
```