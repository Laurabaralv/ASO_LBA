# Proyecto 1ª Evaluación

Para este proyecto se ha configurado el siguiente script, el cual sera explicado más adelante:

```bash

#!/bin/bash

# Solicitar la red a escanear
 
read -p "Introduce la red a escanear en formato CIDR: " RED

# Obtener el nombre del usuario
USUARIO=$(whoami)
ARCHIVO_SALIDA="analisis_red_$USUARIO.txt"

# Limpiar archivo de salida
echo "Analisis de red - $(date)" > "$ARCHIVO_SALIDA"
echo "Red escaneada: $RED" >> "$ARCHIVO_SALIDA"
echo "-----------------------------------" >> "$ARCHIVO_SALIDA"

# Escaneo de equipos conectados
echo "Escaneando equipos conectados..."
nmap -sn "$RED" | grep "Nmap scan report" | awk '{print $5}' > ip_detectadas.txt

echo "Equipos detectados:" >> "$ARCHIVO_SALIDA"
cat ip_detectadas.txt >> "$ARCHIVO_SALIDA"
echo "-----------------------------------" >> "$ARCHIVO_SALIDA"

# Escaneo de puertos abiertos y detección del sistema operativo
echo "Escaneando puertos y detectando sistemas operativos..."
while read -r IP; do
    TTL=$(ping -c 1 "$IP" | grep "ttl=" | awk -F"ttl=" '{print $2}' | awk '{print $1}')
    OS="Desconocido"
    
    if [[ "$TTL" -eq 64 ]]; then
        OS="Linux"
    elif [[ "$TTL" -eq 128 ]]; then
        OS="Windows"
    fi
    
    echo "IP: $IP - Sistema Operativo: $OS" >> "$ARCHIVO_SALIDA"
    echo "Puertos abiertos:" >> "$ARCHIVO_SALIDA"
    nc -zv "$IP" 1-1024 2>&1 | grep "succeeded" | awk '{print $5}' >> "$ARCHIVO_SALIDA"
    echo "-----------------------------------" >> "$ARCHIVO_SALIDA"
done < ip_detectadas.txt

echo "Análisis finalizado. Resultados guardados en $ARCHIVO_SALIDA"
```
Como se menciono anteriormente ahora se comenzara a expicar cada seccion del codigo.
1. Lo primero es solicitar la red que vamos a analizar:
```bash
read -p "Introduce la red a escanear en formato CIDR: " RED
```
2. Seguimos obteniendo el nombre del usuario con 'whoami' , esto para registrar quien solicita la información. Tambien definimos el archivo donde se va a guardar la informacion como variable.
```bash 
echo "Analisis de red - $(date)" > "$ARCHIVO_SALIDA"
echo "Red escaneada: $RED" >> "$ARCHIVO_SALIDA"
echo "-----------------------------------" >> "$ARCHIVO_SALIDA"
```
3. Configuramos que el archivo se sobreescriba y se guarde la fecha y hora junto con la red que se va a escanear.
```bash
echo "Analisis de red - $(date)" > "$ARCHIVO_SALIDA"
echo "Red escaneada: $RED" >> "$ARCHIVO_SALIDA"
echo "-----------------------------------" >> "$ARCHIVO_SALIDA"
```
4. Ahora escaneamos los equipos conectados. ``` nmap -sn "$RED" ``` detecta los host activos. ```grep "Nmap scan report" ``` filtra las líneas del resultado. ```awk '{print $5}' ``` extrae la IP de cada equipo detectado. ```> ip_detectadas.txt ``` Lo guarda en el archivo temporal.
```bash
echo "Escaneando equipos conectados..."
nmap -sn "$RED" | grep "Nmap scan report" | awk '{print $5}' > ip_detectadas.txt
```
```bash
echo "Equipos detectados:" >> "$ARCHIVO_SALIDA"
cat ip_detectadas.txt >> "$ARCHIVO_SALIDA"
echo "-----------------------------------" >> "$ARCHIVO_SALIDA"
```
5. Escaneao de puertos abiertos.
   1. Abrimos el bucle.
   ```bash 
   echo "Escaneando puertos y detectando sistemas operativos..."
   while read -r IP; do
   TTL=$(ping -c 1 "$IP" | grep "ttl=" | awk -F"ttl=" '{print $2}' | awk '{print $1}')
   ```
   2. ``` ping -c 1 "$IP" ``` Envia un paquete ICMP a la IP.
   3. ``` grep "ttl=" ```Filtra las líneas con el valor TTL.
   4. ```awk -F"ttl=" '{print $2}' ``` Se separa la línea en dos y se queda con la segunda parte. 
   5. ```awk '{print $1}' ``` Extrae solpo el numero del TTL.
   6. Ahora definimos a que se le asume el 64 y quien la 128.
   ```bash
   OS="Desconocido"
    
    if [[ "$TTL" -eq 64 ]]; then
        OS="Linux"
    elif [[ "$TTL" -eq 128 ]]; then
        OS="Windows"
    fi
    ```
   7. Se escribe el resultado en el archivo.
   ```bash
   echo "IP: $IP - Sistema Operativo: $OS" >> "$ARCHIVO_SALIDA"
    echo "Puertos abiertos:" >> "$ARCHIVO_SALIDA"
    nc -zv "$IP" 1-1024 2>&1 | grep "succeeded" | awk '{print $5}' >> "$ARCHIVO_SALIDA"
    ```
6. Indicamos que hemos acabado de hacer el analisis.
```bash
echo "Análisis finalizado. Resultados guardados en $ARCHIVO_SALIDA"
```
