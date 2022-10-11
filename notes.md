# ejercicios sobre permisos en linux
Enlace: Archivo PDF en el repositorio

Crea los grupos oficina1 y oficina2.

```bash
addgroup oficina1
addgroup oficina2
```

Crea los usuarios pedro y pablo. Estos usuarios deben pertenecer únicamente al
grupo oficina1.

```bash
sudo adduser pedro

sudo adduser pablo

adduser pedro oficina1
adduser pablo oficina1
```


Crea los usuarios alba y nerea. Estos usuarios deben pertenecer únicamente al
grupo oficina2.

```bash
adduser alba

adduser nerea

adduser alba oficina2
adduser nerea oficina2
```

---

Como usuario pedro Crea un fichero con nombre topsecret.txt al que
únicamente él tenga acceso, tanto de lectura como de escritura.

```bash
su - pedro
cd /home/pedro/

# se escribe el texto que queramos y se guarda
nano topsecret.txt

chmod 600 topsecret.txt
```

Crea otro fichero, también como usuario pedro, con nombre
ventas_trimestre.txt al que tengan acceso, tanto para leer como para escribir
todos los usuarios que pertenezcan al mismo grupo. Comprueba como usuario
pablo que puedes modificar el fichero.

```bash
echo "Pedro was here" > ventas_trimestre.txt
chmod 660 ventas_trimestre.txt
```

** Change the group owner of a file by using the chgrp command.`chgrp group filename`

```bash
chgrp oficina1 ventas_trimestre.txt
```

---

Como usuario alba, crea un fichero con nombre empleados.txt al que pueda acceder
cualquier usuario para leer su contenido, y cualquier usuario del mismo grupo para
leer o escribir .
Su alba

```bash
su -u alba
echo "Alba was here" > empleados.txt
chmod 764 empleados.txt
```

** Agregar el usuario pc4(alumno)
```bash
sudo adduser pc4
```


Copia el fichero empleados.txt al directorio de trabajo de alumno. Cambia el
propietario y el grupo al que pertenece el fichero, ahora debe ser alumno.

```bash
sudo cp empleados.txt /home/pc4
sudo chown pc4 empleados.txt
sudo chgrp pc4 empleados.txt
```

---

Como usuario pablo, copia un programa del directorio /usr/bin al directorio de
trabajo con un nombre
diferente. Por ejemplo kalarm se puede copiar como alarma. Mira los
permisos de este programa. Comprueba que se puede ejecutar .

```bash
su pablo
cp /usr/bin/kalarm /home/pablo/alarma
ls -l /home/pablo/alarma

# -rwxr-xr-x 1 pablo pablo 30904 Oct 11 20:27 /home/pablo/alarma
```

Cambia los permisos de alarma de tal f orma que sólo lo pueda ejecutar el
propietario del archivo.

```bash
chmod 744 /home/pablo/alarma
# -rwxr--r-- 1 pablo pablo 30904 Oct 11 20:27 /home/pablo/alarma
```
---

Crea el usuario modesto, perteneciente a oficina2. Dentro de su
directorio de trabajo, crea un directorio de nombre compartido_con_todos.

```bash
sudo adduser modesto
sudo adduser modesto oficina2
su modesto
cd 
mkdir compartido_con_todos
```


Dentro de ese directorio, edita con el OpenOffice los ficheros
telefono_contactos, gastos_marzo y sueldos. Inserta varias entradas en cada uno de
los ficheros.

```bash
cd compartido_con_todos
echo "9999999999" >> telefonos_de_contactos.txt
echo "8888888888" >> telefonos_de_contactos.txt
echo "7777777777" >> telefonos_de_contactos.txt

echo "g01" >> gastos_marzo.txt
echo "g02" >> gastos_marzo.txt
echo "g03" >> gastos_marzo.txt

echo "s01" >> sueldos.txt
echo "s02" >> sueldos.txt
echo "s03" >> sueldos.txt
```

12.
Da permiso de lectura a la carpeta compartido_con_todos y a todos los
ficheros que contenga para todos los usuarios.
```bash
chmod -R 744 compartido_con_todos/
chmod -R u+rwx, g+r-w, o+r-w compartido_con_todos
```


# EJERCICIO Y EJEMPLOS DE PERMISOS GNU / LINUX

Enlace: https://www.codifica.me/ejercicio-y-ejemplos-de-permisos-gnu-linux/

Creación con root del directorio clase
 
```bash
su

cd /

mkdir clase
chmod 777 clase
```

Creación de usuarios y grupos

```bash
adduser profesor
adduser alumno1
adduser alumno2
adduser alumno3

addgroup alumnos
addgroup profesores
```

Ahora se debe asignar los grupos a cada usuario. Como ambos ya están creados usamos usermod -a -G grupo usuario.

```bash
usermod -a -G alumnos alumno1
usermod -a -G alumnos alumno2
usermod -a -G alumnos alumno3

usermod -a -G profesores profesor
```


Creación de carpetas con el profesor

```bash
su profesor
mkdir /clase/trabajos
chmod 775 /clase/trabajos


mkdir /clase/examenes
chmod 770 /clase/examenes


mkdir /clase/buzon
chmod 777 /clase/buzon
ls -l /clase
```


Creación de archivos con el profesor

```bash
touch /clase/trabajos/tarea1.txt
touch /clase/examenes/junio.txt
touch /clase/buzon/enlaces.txt
```

Comprobando permisos con alumno1
```bash
su alumno1

head /clase/trabajos/tarea1.txt

echo "escribiendo" > /clase/trabajos/tarea1.txt
# bash: /clase/trabajos/tarea1.txt: Permission denied


```

Para el directorio examenes:
```bash
head /clase/examenes/junio.txt
# head: cannot open '/clase/examenes/junio.txt' for reading: Permission denied

echo "escribiendo" > /clase/examenes/junio.txt
# bash: /clase/examenes/junio.txt: Permission denied
```

Para el directorio buzon:
```bash
echo "escribiendo" > /clase/buzon/enlaces.txt
# bash: /clase/buzon/enlaces.txt: Permission denied

touch /clase/buzon/ejemplos.txt
```