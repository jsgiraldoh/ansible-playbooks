Ansible
===

Ansible es un software que automatiza el aprovisionamiento de software, la gestión de configuraciones y el despliegue de aplicaciones. Está categorizado como una herramienta de orquestación, muy útil para los administradores de sistema y DevOps.

En otras palabras, Ansible permite a los DevOps gestionar sus servidores, configuraciones y aplicaciones de forma sencilla, robusta y paralela.

Automatice la implementación y administración de toda su infraestructura de TI.


## Instalación de Ansible en RHEL/CentOS – (Ansible Server)

Para comenzar es una recomendación, pero no obligatoria, actualizar el sistema operativo.

```
yum update -y
```

Por defecto Ansible no se encuentra en los repositorios predeterminados de RHEL. Como puede haber experimentado al instalar herramientas en el pasado, a menudo se requiere que se instale el Paquete Extra para Enterprise Linux (EPEL) antes de utilizar el administrador de paquetes para instalar Ansible. Este es un paso muy sencillo. En primer lugar, hay que descargar el archivo rpm epel-release desde el sitio web del Proyecto Fedora.

```
yum install https://dl.fedoraproject.org/pub/epel/epel- release-latest-7.noarch.rpm
 ```

Una vez añadido el repositorio EPEL, es posible descargar Ansible.

```
yum install ansible -y
```

Para verificar la versión de ansible que se tiene instalado en el servidor, ejecutamos el siguiente comando.

```     
ansible --version
```

## Creación de usuarios – (Ansible Nodos)
Para poder gestionar los nodos clientes, se debe realizar una conexión SSH para ello habilitaremos un usuario.

```
useradd user-ansible
echo “ose2020” | passwd user-ansible --stdin
```

Editamos el archivo visudo, para habilitar los permisos al nuevo usuario.

```
visudo
...
user-ansible ALL=(ALL) NOPASSWD: ALL
```

## Creación y copia de llave SSH – (Ansible Server)

Para Ansible confía en SSH para comunicarse con sus clientes. La configuración se debe realizar en el nodo maestro para crear una clave SSH que luego se copia a todos los hosts del cliente para habilitar el acceso remoto sin contraseña. Debe crearse una clave SSH.

```
ssh-keygen -b 2048 -t rsa
```

Ya con la llave creada, se debe copiar la llave publica al usuario creado anteriormente en los nodos clientes.

```
ssh-copy-id user-ansible@192.168.1.X
ssh-copy-id user-ansible@192.168.1.Y
```

# Referencias

https://docs.ansible.com/ansible/latest/user_guide/playbooks_vars_facts.html

http://www.osenterprise.com.pe/web/
