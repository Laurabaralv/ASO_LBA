# PR0302: Comando Case

1.Menú de operaciones matemáticas

```bash
#!/bin/bash

read -p "Dime el primer operario: " n1
read -p "Dime el segundo operario: " n2
read -p "Dime la operacion que quieres realizar: " op

case $op in
        +)
                echo "El resultado es $(($n1 + $n2))";;
        -)
                echo "El resultado es $(($n1 - $n2))";;
        \*)
                echo "El resultado es $(($n1 * $n2))";;
        /)
                echo "El resultado es $(($n1 / $n2))";;
esac
```

2.Verificar dias de la semana

```bash
#!/bin/bash

read -p "Dime un dia de la semana: " dia

case $dia in
        lunes| martes | miercoles | jueves | viernes)
                echo "Es un da laboral";;
        sabado | domingo)
                echo "Es fin de semana";;
esac
```

3.Clasificar calificaciones

```bash
#!/bin/bash

read -p "dime tu nota: " n

case $n in
        9 | 10)
                echo "Sobresaliente";;
        7 | 8)
                echo "notable";;
        6)
                echo "bien";;
        5)
                echo "suficiente";;
        [0-4])
                echo "suspenso";;
esac
```

4.Determinar la estación del año

```bash
#!/bin/bash

read -p "dime un mes del año: " mes

case $mes in
        enero | febrero | marzo)
                echo "Es invierno";;
        abril | mayo | junio)
                echo "Es primavera";;
        julio | agosto | septiembre)
                echo "Es verano";;
        octubre | noviembre | diciembre)
                echo "Es otoño";;
esac
```

5.Identificar el tipo de archivo

```bash
#!/bin/bash

read -p "Dime la extension del archivo: " ext

case $ext in
        .txt)
                echo "es un texto";;
        .jpg)
                echo "es una imagen";;
        .pdf)
                echo "es un PDF";;
        .???)
                echo "es otro tipo de archivo";;
esac
```

6.Convertir temperaturas

```bash
#!/bin/bash

clear
echo "Dime qué operación quieres realizar:"
echo "   1 - Convertir Celsius a Fahrenheit"
echo "   2 - Convertir Fahrenheit a Celsius"
read -p "Elige una opción: " conv
read -p "Dime la temperatura que quieres calcular: " temp

case $conv in
        1)
                echo "Son $(($temp * 2 + 32))";;
        2)
                echo "Son $(($temp - 32 / 2 ))";;
esac
```

7.Estado del servicio

script18.sh
```bash
#!/bin/bash 

read -p "Por favor, introduzca el nombre del servicio (por ejemplo, apache o mysql): " servicio

echo "Selecciona una opción para el servicio '$servicio':"
echo "1. Iniciar el servicio"
echo "2. Detener el servicio"
echo "3. Reiniciar el servicio"
echo "4. Salir"

read -p "Introduzca su opción (1/2/3/4): " opcion

case $opcion in
    1)
        echo "Iniciando el servicio '$servicio'..."
        sudo systemctl start $servicio
        ;;
    2)
        echo "Deteniendo el servicio '$servicio'..."
        sudo systemctl stop $servicio
        ;;
    3)
        echo "Reiniciando el servicio '$servicio'..."
        sudo systemctl restart $servicio
        ;;
    4)
        echo "Saliendo del script..."
        exit 0
        ;;
    *)
        echo "Opción no válida. Por favor, seleccione 1, 2, 3 o 4."
        ;;
esac
```

8.Conversión de unidades de longitud

```bash
#!/bin/bash

read -p "Introduce el valor en metros: " metros

if ! [[ "$metros" =~ ^[0-9]+(\.[0-9]+)?$ ]]; then
    echo "Por favor, introduce un número válido."
    exit 1
fi

echo "Selecciona una opción de conversión:"
echo "1. Convertir metros a kilómetros"
echo "2. Convertir metros a centímetros"
echo "3. Convertir metros a milímetros"
echo "4. Salir"

read -p "Introduce tu opción (1/2/3/4): " opcion

case $opcion in
    1)
        kilometros=$(echo "$metros / 1000" | bc -l)
        echo "$metros metros son $kilometros kilómetros."
        ;;
    2)
        centimetros=$(echo "$metros * 100" | bc)
        echo "$metros metros son $centimetros centímetros."
        ;;
    3)
        milimetros=$(echo "$metros * 1000" | bc)
        echo "$metros metros son $milimetros milímetros."
        ;;
    4)
        echo "Saliendo del script..."
        exit 0
        ;;
    *)
        echo "Opción no válida. Por favor, seleccione 1, 2, 3 o 4."
        ;;
esac
```   