# SI-Bitacora3-AccesoRemoto
## 2. Despliegue de la Infraestructura
Para comenzar el laboratorio, utilicé Docker Compose para levantar dos servidores independientes.

Comando utilizado: docker-compose up -d

Resultado: Se crearon dos contenedores:

lab_ssh_servidor: Servidor Linux accesible por el puerto 2222.

lab_rdp_servidor: Servidor con entorno gráfico (Ubuntu XFCE) en los puertos 3000 (Web) y 3389 (RDP).
<img width="1092" height="141" alt="image" src="https://github.com/user-attachments/assets/15d5542f-d79d-44f4-a2e8-9c1268bf8e78" />

## 3. Configuración de SSH (Tarea 3.1)
En esta fase, configuramos un acceso seguro mediante criptografía de clave pública. El objetivo es eliminar la necesidad de contraseñas, aumentando la seguridad y permitiendo automatizaciones.

Paso A: Conexión Inicial
Me conecté por primera vez al servidor de Dublín (el contenedor) para verificar la conectividad a través del túnel seguro.

Comando: ssh alumno@localhost -p 2222

Credenciales: Usuario alumno / Contraseña sistemas_informaticos.

Paso B: Generación de Identidad
Generé un par de llaves criptográficas en mi máquina anfitriona (Windows) utilizando el algoritmo Ed25519, que es más eficiente y seguro que el antiguo RSA.
<img width="288" height="236" alt="image" src="https://github.com/user-attachments/assets/51060146-6544-450f-adc0-18a5c5edb814" />


Comando: ssh-keygen -t ed25519 -C "tu_correo@ejemplo.com"

Paso C: Transferencia de la Llave
Dado que el comando ssh-copy-id no estaba disponible de forma nativa en mi terminal de Windows, realicé la transferencia de forma manual para autorizar mi llave pública en el servidor.

Visualicé mi llave pública con type %USERPROFILE%\.ssh\id_ed25519.pub.

La añadí al archivo ~/.ssh/authorized_keys dentro del servidor.

Ajusté los permisos con chmod 600 para asegurar que solo el propietario pueda leer la llave.
Ya se puede acceder sin que nos pida la contraseña con exito:
<img width="744" height="72" alt="image" src="https://github.com/user-attachments/assets/7e1c3a07-4e58-41f9-befc-d15fe6a0cbe8" />

## 3. Configuración de SSH (Tarea 3.2)
En esta fase, exploramos la administración mediante Interfaz Gráfica de Usuario (GUI). Aunque la terminal es más eficiente, el entorno gráfico es vital para aplicaciones específicas o para usuarios que no dominan la línea de comandos.

Acceso y Configuración
Conexión vía Web: Utilicé el puerto 3000 para acceder al escritorio a través del navegador. Esto es posible gracias a que el contenedor integra un servidor web que traduce el protocolo gráfico a HTTP.

Prueba de persistencia: Para demostrar la interacción con el sistema, realicé las siguientes acciones:

Incidencia y Solución
Problema: Al intentar la conexión mediante el cliente de Escritorio Remoto estándar (MSTSC/RDP) apuntando a localhost:3389, surgieron problemas de compatibilidad/conexión (la "primera opción" no permitía el acceso directo).

Solución: Opté por la vía alternativa utilizando el puerto 3000. Este puerto expone una interfaz web (Apache Guacamole) que encapsula el protocolo gráfico en tráfico HTTP, lo cual resultó ser mucho más fluido y compatible con el navegador.

Creé un archivo en el escritorio denominado PRUEBA_LOGRADA.txt.

Escribí un mensaje de confirmación dentro del archivo.

<img width="1915" height="986" alt="image" src="https://github.com/user-attachments/assets/7ebed303-ab24-423e-8e7a-8fc381d3667b" />
