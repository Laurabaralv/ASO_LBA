# PR0303: Ejercicios sobre comandos while, until y for

1. Contar hasta 10 con for

```bash 
#!/bin/bash

for var in {1..10}
do
        echo "el siguiente numero es $var"
done

```

2. Sumar los primeros 50 números

```bash 
#/bin/bash

for suma in {0..50}
do
        echo "$suma + $suma = $(($suma + $suma))"
done
```

3. Tabla de multiplicar

```bash 
#!/bin/bash

read -p "dime un numero para saber su tabla de multiplicar: " num

for mul in {0..10}
do
        echo "$num * $mul = $(($num * $mul)) "
done

```

4. Imprimir cada letra  
script 23

```bash 

```

5. Contar números pares del 1 al 20 con while

```bash 
#!/bin/bash

# Inicializar la variable con el primer número
numero=2

# Usar un bucle 'while' para mostrar los números pares entre 1 y 20
while [ $numero -le 20 ]; do
    echo $numero
    # Incrementar en 2 para obtener el siguiente número par
    numero=$((numero + 2))
done

```

6. Suma de digitos



7. Cuenta regresiva

```bash 

#!/bin/bash

read -p "dime un numero: " num

until [ $num -le 0 ]
do
        echo "$num"
        num=$(( $num - 1 ))
done

```

8. Imprimir solo archivos .txt

```bash 

#!/bin/bash

read -p "dime un directorio" directorio

for archivo in $directorio
do
        if [[ $archivo == .txt ]]
        then
                echo "$archivo"
        fi
done

```

9. Factorial de un número
script28

```bash 

#!/bin/bash
read -p "Introduce un numero: " num
 
fact=1
for i in $(seq 2 $num)
do
   fact=$(( fact * i  ))
done
echo El factorial de $num es $fact

```

10.  Verificar contraseña

```bash 
#!/bin/bash

# Definir la contraseña correcta
contraseña_correcta="secreta123"

# Pedir al usuario la contraseña
until [ "$entrada" == "$contraseña_correcta" ]; do
    read -sp "Introduce la contraseña: " entrada
    echo  # Para saltar una línea después de la entrada
    if [ "$entrada" != "$contraseña_correcta" ]; then
        echo "Contraseña incorrecta. Intenta nuevamente."
    fi
done

echo "Contraseña correcta. Acceso permitido."
```

11. Adivinar un número

```bash 
#!/bin/bash

# Generar un número aleatorio entre 1 y 10
numero_correcto=$((RANDOM % 10 + 1))

# Pedir al usuario que adivine el número
echo "Bienvenido al juego. Adivina el número entre 1 y 10."

# Inicializar la variable para la adivinanza del usuario
adivinanza=0

# Usar 'while' para seguir pidiendo el número hasta que lo adivine
while [ $adivinanza -ne $numero_correcto ]; do
    read -p "Introduce tu adivinanza: " adivinanza

    # Verificar si la adivinanza es incorrecta
    if [ $adivinanza -lt $numero_correcto ]; then
        echo "Demasiado bajo. Intenta nuevamente."
    elif [ $adivinanza -gt $numero_correcto ]; then
        echo "Demasiado alto. Intenta nuevamente."
    fi
done

# Mensaje de éxito cuando el usuario adivina correctamente
echo "¡Felicidades! Adivinaste el número correctamente: $numero_correcto."
```

12. Mostrar la fecha n veces

```bash 

```

13. Promedio de números ingresados

```bash 

read -p "Introduce un numero: " num

suma=0 
cont=0
while [ $num != "fin" ]
do
        suma=$(( $suma + $num ))
        cont=$(( $cont + 1 ))
        read -p "Introduce un numero: " num
done
echo has introducido $cont numeros
echo su suma es $suma
echo y sy promedio es $(( $suma / $cont ))

```

14. Contar palabras en una cadena

```bash 
#!/bin/bash

# Solicitar al usuario una frase
read -p "Introduce una frase: " frase

# Inicializar el contador de palabras
contador=0

# Usar el bucle 'for' para iterar sobre las palabras en la frase
for palabra in $frase; do
    # Incrementar el contador por cada palabra
    contador=$((contador + 1))
done

# Mostrar el número de palabras
echo "La frase tiene $contador palabras."
```

15. Juego de adivinar con límites dinámicos

```bash 
#!/bin/bash

# Generar un número aleatorio entre 1 y 100
numero_correcto=$((RANDOM % 100 + 1))

# Mensaje introductorio
echo "Adivina el número entre 1 y 100."

# Inicializar la variable para la adivinanza del usuario
adivinanza=0

# Usar 'while' para seguir pidiendo el número hasta que lo adivine
while [ $adivinanza -ne $numero_correcto ]; do
    # Solicitar un intento al usuario
    read -p "Introduce tu adivinanza: " adivinanza

    # Comprobar si la adivinanza es incorrecta
    if [ $adivinanza -lt $numero_correcto ]; then
        echo "Demasiado bajo. Intenta nuevamente."
    elif [ $adivinanza -gt $numero_correcto ]; then
        echo "Demasiado alto. Intenta nuevamente."
    fi
done

# Mensaje de éxito cuando el usuario adivina correctamente
echo "¡Felicidades! Adivinaste el número correctamente: $numero_correcto."
```

16. Archivos con nombres de directorios

```bash 

ruta=$(pwd)

for f in $ruta/*
do
        if [ -d $f ]
        then
                echo $f >> ./directorios.txt
        fi
done

```

17. Generar archivos de texto numerados

```bash 
#!/bin/bash

# Solicitar al usuario un número 'n'
read -p "Introduce el número de archivos a crear: " n

# Verificar si la entrada es un número válido
if ! [[ "$n" =~ ^[0-9]+$ ]] || [ "$n" -le 0 ]; then
    echo "Por favor, introduce un número válido mayor que 0."
    exit 1
fi

# Usar un bucle 'for' para generar los archivos
for ((i=1; i<=n; i++)); do
    # Crear el archivo con el nombre "archivoX.txt"
    touch "archivo$i.txt"
    echo "Archivo archivo$i.txt creado."
done

echo "Se han creado $n archivos."
```

18. Conteo de vocales en una cadena



19. Validación de entrada

```bash 
#!/bin/bash

# Usar until para pedir un número entre 1 y 10
until [[ "$numero" =~ ^[1-9]$|^10$ ]]; do
    # Solicitar al usuario que ingrese un número entre 1 y 10
    read -p "Introduce un número entre 1 y 10: " numero

    # Verificar si el número es válido (entre 1 y 10)
    if ! [[ "$numero" =~ ^[1-9]$|^10$ ]]; then
        echo "Número inválido. Debes ingresar un número entre 1 y 10."
    fi
done
```

20. Script de copia de seguridad

```bash 
#!/bin/bash

# Solicitar al usuario el directorio de origen
read -p "Introduce el directorio de origen: " directorio_origen

# Verificar si el directorio existe
if [ ! -d "$directorio_origen" ]; then
    echo "El directorio especificado no existe. Saliendo..."
    exit 1
fi

# Crear la carpeta de backup si no existe
backup_dir="backup"
if [ ! -d "$backup_dir" ]; then
    mkdir "$backup_dir"
    echo "Se ha creado la carpeta de respaldo: $backup_dir"
fi

# Usar 'for' para recorrer los archivos en el directorio
for archivo in "$directorio_origen"/*.txt; do
    # Verificar si es un archivo .txt
    if [ -f "$archivo" ]; then
        # Copiar el archivo a la carpeta de respaldo
        cp "$archivo" "$backup_dir/"
        echo "Archivo $archivo copiado a $backup_dir/"
    fi
done

echo "Copia completada."

```