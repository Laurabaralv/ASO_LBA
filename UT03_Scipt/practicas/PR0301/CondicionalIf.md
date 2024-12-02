# PR0301: Concicional if

1.Comprobación del número par o impar

```bash
#!/bin/bash

read -p "dime un numero: " n
if [ $(( $n%2 )) -eq 0 ]
then
echo "El numero $n es par"
else
echo "El numero $n es impar"
fi
```

2.Verificación de archivo

```bash
#!/bin/bash

read -p "Dime la ruta del archivo: " archivo

if [ -e $archivo ]
then
echo "El archivo $archivo existe y tiene permisos de escritura"
else
echo "El archivo $archivo existe pero no tiene permisos de escritura"
fi
```

3.Comprobación de dos números

```bash
#!/bin/bash

read -p "Dime el primer numero: " n1
read -p "Dime el segundo numero: " n2

if [ $n1 -eq $n2 ]
then
   echo "el numero $n1 es igual a $n2"
else
   if [ $n1 -gt $n2 ]
   then
        echo "el numero $n1 es mayor que $n2"
   else
        echo "el numero $n2 es mayor que $n1"
   fi
fi
```

4.Validación de contraseña

```bash
#!/bin/bash

read -p "dime tu cosntraseña: " pass
secret=1234
if [ $pass = $secret ]
then
        echo "la contraseña es correcta"
else
        echo "la contraseña no es correcta"
fi
```

5.Comprobación de directorio

```bash
#!/bin/bash

read -p "Dime un fichero: " f
if [ -r $f ]
    then
        echo "el fichero existe y tiene permisos de escritura"
    else
        echo "Creando fichero nuevo"
        date > /home/$f
fi

```

6.Verificar si el usuario es root

```bash
#!/bin/bash

if [ $(whoami) = "root" ]
the 
    echo "Eres root"
else
    echo "no eres root"
fi
```

7.Calificación de un examen

```bash
#!/bin/bash
read -p "Dime la nota: " n

if [ $n -ge 5 ]
then
     echo "Aprobado"
else
    if [ $n -lt 5 ]
    then
    echo "Suspenso"
    fi
fi
```

8.Comprobación del espacio de trabajo

```bash
#!/bin/bash

espacio_libre=$(df / | tail -1 | awk '{print $5}' | sed 's/%//')

if [ $espacio_libre -lt 10 ]; then
    echo "Advertencia: El espacio libre en disco es inferior al 10%. Queda solo $espacio_libre% de espacio libre."
else
    echo "El espacio libre en disco es suficiente. Queda $espacio_libre% de espacio libre."
fi

```

9.Menú de opciones

```bash
#!/bin/bash

# Mostrar el menú
echo "Seleccione una opción:"
echo "1. Ver la fecha y hora actual"
echo "2. Mostrar el espacio libre en disco"
echo "3. Salir"

read -p "Introduzca su opción (1/2/3): " opcion

case $opcion in
    1)
        echo "La fecha y hora actual es: $(date)" ;;
    2)
        echo "El espacio libre en disco es:"
        df -h ;;
    3)
        echo "Saliendo del script..."
        exit 0 ;;
    *)
        echo "Opción no válida. Por favor, seleccione 1, 2 o 3." ;;
esac

```

10.Evaluación de edad

```bash
#!/bin/bash

read -p "Por favor, introduzca su edad: " edad

if ! [[ "$edad" =~ ^[0-9]+$ ]]; then
    echo "Por favor, introduzca un número válido."
    exit 1
fi

if [ $edad -lt 18 ]; then
    echo "Eres menor de edad."
elif [ $edad -ge 18 ] && [ $edad -le 65 ]; then
    echo "Eres adulto."
else
    echo "Eres mayor de edad."
fi

```

11.Contar líneas de un archivo

```bash
#!/bin/bash

read -p "Por favor, introduzca el nombre del archivo: " archivo

if [ ! -f "$archivo" ]; then
    echo "El archivo '$archivo' no existe o no es un archivo regular."
    exit 1
fi

lineas=$(wc -l < "$archivo")

echo "El archivo '$archivo' tiene $lineas líneas."

```