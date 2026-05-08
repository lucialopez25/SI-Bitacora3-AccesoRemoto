# SI-Bitacora3-AccesoRemoto
## 1. Despliegue de la Infraestructura
Para comenzar el laboratorio, utilicé Docker Compose para levantar dos servidores independientes.

Comando utilizado: docker-compose up -d

Resultado: Se crearon dos contenedores:

lab_ssh_servidor: Servidor Linux accesible por el puerto 2222.

lab_rdp_servidor: Servidor con entorno gráfico (Ubuntu XFCE) en los puertos 3000 (Web) y 3389 (RDP).
<img width="1092" height="141" alt="image" src="https://github.com/user-attachments/assets/15d5542f-d79d-44f4-a2e8-9c1268bf8e78" />

## 2. Configuración de SSH (Tarea 3.1)
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
