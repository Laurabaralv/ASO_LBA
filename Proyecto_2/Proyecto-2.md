# Proyecto 2ª Evaluación

## Introducción

Para este proyecto tenemos que recrear la administración de dominio perteneciente a un centro educativo.
Todo esto se ha realizado sobre una máquina virtual de Windows Server 2019, la cual ha sido pomovida a dominioy añadido el rol 'Servicios de archivos y almacenamiento'. Para administras correctamente el servidor

## Estructura del dominio
A continuación, se expondra la estructuración y configuración que se ha realizado a este dominio.

### Unidades Organizativas
Primero comenzamos con las Unidades Organizativas que hemos creado. Hemos creado una en la que guardaremos todo lo relacionado con el centro educativo pues puede haber usuarios que no formen parte del centro como pueden ser los tecnicos informáticos.

Dentro de la UO CentroEducativo hemos creado otras tres UO, una para los usuarios, otra para los equipos y otra para los grupos.
La UO alumnos contrentra la UO Profesores y la UO alumnos, esta a su vez esta compuestas por otras UO correspondientes a cada grado que se imparte y poseen cada una UOs correspondientes a los cursos que haya.

La UO equipos posee las UOs Aulas y Administracion.
Por último, la UO Grupos posee los grupos alumnos y Profesores.
Entonces nos quedaria la siguiente estructura en las Unidades Organizativas:

- OU=CentroEducativo  
  - OU=Usuarios
    - OU=Alumnos
      - OU=ASIR
        - OU=Primero
        - OU=Segundo
      - OU=SMR
        - OU=Primero
        - OU=Segundo
      - OU=DAM
        - OU=Primero
        - OU=Segundo
      - OU=DAW 
        - OU=Primero
        - OU=Segundo
    - OU=Profesores
  - OU=Equipos
    - OU=Aulas
      - OU=Aula1
      - OU=Aula2
      - OU=Aula3
      - OU=Aula4
    - OU=Administracion
  - OU=Grupos
    - Grupo_Alumnos
    - Grupo_Profesores

## Script para incorporar los alumnos

Para este proyecto se nos ha facilitado un documento con la información de los alumnos, debido a la extension de este la mejor opcion para incorporar al alumnado al dominio es mediante un script ya que si se hacia manualmente se tardaría demasiado tiempo.

Este script lo hemos creado en una carpeta denomidada Administracion y a la que hemos modificado los permisos para que solo puedan acceder a esta los administradores y profesorado que pertenezca a la UO de ADministracion, pues si se inscriven nuevos alumnos solo tienen que incorporarlos en el fichero 'alumnos.csv' que tambien estara en esta carpeta y ejecutar el script. 

Tambien se puede crear en esta carpeta un documento de texto con los pasos para ejecutar el script en caso de que haya alguien que no sepa o se le olvide el como hacerlo.

El script en cuestion tiene la siguiente configuración, no solo incorpora los alumnos sino que tambien crea las carpetas personales:
```bash

Import-Csv "alumnos.csv" | ForEach-Object {
# Variables para que los datos del .csv se puedan automatizar
    $nombre = $_.Nombre
    $apellido1 = $_.PrimerApellido
    $apellido2 = $_.SegundoApellido
    $usuario = ($nombre.Substring(0,1) + $apellido1).ToLower()
    $password = "Pass1234"
    $ciclo = $_.Ciclo
    $curso = $_.Curso
    $ou = "OU=$curso,OU=$ciclo,OU=Alumnos,OU=Usuarios,DC=centro,DC=local"
    
# creacion de los usuarios    
    New-ADUser -Name "$nombre $apellido1 $apellido2" -GivenName $nombre -Surname "$apellido1 $apellido2" -SamAccountName $usuario \
    -UserPrincipalName "$usuario@centro.local" -Path $ou -AccountPassword (ConvertTo-SecureString $password -AsPlainText -Force) -Enabled $true

# Creacion de la carpeta personal y añadir a los alumnos en dus respectivos grupos
    $carpetaPersonal = "\\Servidor\Compartido\$usuario"
    New-Item -Path $carpetaPersonal -ItemType Directory
    icacls $carpetaPersonal /grant "$usuario`:(OI)(CI)F"
}

$grupos = @("ASIR_Primero", "ASIR_Segundo", "DAM_Primero", "DAM_Segundo")
foreach ($grupo in $grupos) {
    $rutaGrupo = "\\Servidor\Compartido\$grupo"
    New-Item -Path $rutaGrupo -ItemType Directory
    icacls $rutaGrupo /grant "Centro\$grupo`:(OI)(CI)F"
}
```
## Politicas de seguridad

Se han tomado las siguientes medidas para el dominio:
- Restricción del uso de CMD para alumnos
- Bloqueo del acceso a configuraciones críticas
- Contraseñas robustas (mínimo 8 caracteres, caducidad en 90 días)
- Inicio de sesión restringido a aulas correspondientes

Todo esto lo hemos configuraso a traves de la herramienta de 'administración de directivas de Activity Directory'. Pues no todos los usuarios en especial los alumnos van a tener permitido acceder a todos lados.