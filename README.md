# Taller Linux

Repositorio correspondiente al trabajo práctico de administración y automatización de servidores Linux mediante **Ansible**.

## Requisitos

Para ejecutar los playbooks es necesario contar con:

* **Ansible**
* Acceso SSH a los servidores definidos en el inventario.
* Las colecciones de Ansible especificadas en `collections/requirements.yaml`.

Para instalar las colecciones requeridas:

```bash
ansible-galaxy collection install -r collections/requirements.yaml
```

Además, el proyecto utiliza **Ansible Vault** para proteger las credenciales de la base de datos.

## Playbooks

### `hardening.yaml`

Realiza tareas de hardening y configuración inicial de los servidores Ubuntu, incluyendo:

* Actualización de paquetes.
* Configuración del firewall mediante UFW.
* Instalación y configuración de Fail2ban.
* Aplicación de medidas básicas de seguridad.

### `ubuntu_database.yaml`

Configura los servidores Ubuntu destinados a funcionar como servidores de base de datos:

* Instalación y configuración de MariaDB.
* Creación de la base de datos y usuarios.
* Importación de la base de datos inicial.
* Configuración de permisos.
* Restricción del acceso a MariaDB mediante firewall.

### `apache_php.yaml`

Configura los servidores CentOS destinados a funcionar como servidores web:

* Instalación de Apache.
* Instalación y configuración de PHP/PHP-FPM.
* Configuración del firewall mediante Firewalld.
* Despliegue de la aplicación.
* Configuración de SELinux para permitir la comunicación con la base de datos.

## Ejecución

Los playbooks se ejecutan utilizando el inventario ubicado en `inventory/hosts.ini`.

### Hardening de Ubuntu

```bash
ansible-playbook -i inventory/hosts.ini playbooks/hardening.yaml --ask-become-pass
```

### Configuración de la base de datos

```bash
ansible-playbook -i inventory/hosts.ini playbooks/ubuntu_database.yaml --ask-become-pass --ask-vault-pass
```

### Configuración de Apache y PHP

```bash
ansible-playbook -i inventory/hosts.ini playbooks/apache_php.yaml --ask-become-pass --ask-vault-pass
```

## Estructura

```text
tallerlinux/
├── collections/
├── files/
├── inventory/
├── playbooks/
├── templates/
├── vars/
├── LICENSE
└── README.md
```
