#  PR0204: Programación de tareas con cron

1. ¿Qué orden pondrías en crontab en los siguientes casos?

La tarea se ejecuta cada hora --> 0 * * * *

La tarea se ejecuta los domingos cada 3 horas --> 0 */3 * * 0

La tarea se ejecuta a las 12 de la mañana los días pares del mes. --> 0 12 */2 * *

La tarea se ejecuta el primer día de cada mes a las 8 de la mañana y a las 8 de la tarde. --> 0 8,20 1 * *

La tarea se ejecuta cada media hora de lunes a viernes. --> */30 * * * 1-5

La tarea se ejecuta cada cuarto de hora, entre las 3 y las 8, de lunes a viernes, durante todo el mes de agosto --> */15 3-8 * 8 1-5

La tarea se ejecuta cada 90 minutos --> */30 1,4,7,* *



1. ¿Cómo compruebas si el servicio cron se está ejecutando?

Lo podemos buscar con el comando:

```
ps aux |grep cron |grep -v grep
```

o con

```
systemctl status cron
```


3. ¿Cuál es el efecto de la siguiente línea crontab?
 
    ```
    */15 1,2,3 * * * who > /tmp/test
    ```

Que cada 15 minutos a las horas 1, 2 y 3 sobreescriba el fichero con los usuarios que esten conectdos.

4. Indica la ruta del fichero crontab del sistema

```
ls /etc/crontab
```

5. ¿Qué ficheros controlan los usuarios que pueden utilizar el crontab?



6. Excepcionalmente se debe iniciar una tarea llamada script.sh todos los lunes a las 07:30h antes de entrar en clase ¿Cómo lo harías?

crontab-e

```
*/30 7 * * 1 script.sh
``` 

1. Se ha cancelado la tarea. ¿Cómo listar y luego, suprimir la tarea?

crontab -l --> para listarlo

crontab -r --> para eliminar

8. Ejecuta el comando ps -ef para el usuario root cada 2 minutos y redirecciona el resultado a /tmp/ps_result sin sobrescribir los antiguos.

```
crontab -e

*/2 * * * * * sudo ps -ef >> /tmp/ps_result
```

o ejecutar 

```
sudo crontab -e 

*/2 * * * * * ps -ef >> /tmp/ps_result
```

9.  Verifica la lista de tareas en crontab

10.Espera unos minutos y comprueba el resultado en /tmp



11. Crea el usuario asir2 y prohíbele utilizar el crontab.

```
sudo asir2 > /etc/cron.deny
```

12. Verifica que el usuario asir2 realmente no puede utilizar crontab

iniciamos sasion con el usuario asir2  y se prueba a crear una tarea, lo cual no dejara hacer y nos saldra un mensaje donde indica que este usuario no puede hacerlo.

13. Programa crontab para que cada día a las 0:05 se eliminen todos los ficheros que se encuentran en el directorio /tmp.

```
crontab -e

*/5 * * * * 0-6 rm -f /tmp
```

14. Programa una tarea en el sistema que se lance de lunes a viernes a las 9 de la mañana durante los meses de verano (julio, agosto y septiembre) que escriba en un fichero la hora actual (comando date, aunque tienes que mirar la ayuda para elegir un formato comprensible) seguido del listado de usuarios que hay conectados en ese momento en el sistema (comando who)

```
date '+%T'
```

15. El servicio cron se ayuda de una serie de ficheros y directorios que se encuentran en el directorio /etc. Explica la función de cada uno de los siguientes ficheros/directorios:

- cron.d: 
- cron.allow: si existe permite que solo los usuarios en el listado de dicho fichero pueden crear, editar, mostrar o eliminar ficheros crontab. Sino existe todos los usuarios pueden hacerlo.
- cron.deny: 
- cron.daily: ejecutar una vez.
- cron.hourly: ejecutar cada hora.
- cron.monthly:  ejecutar una vez al mes.
