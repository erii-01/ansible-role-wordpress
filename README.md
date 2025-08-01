[![Ansible Role Test with Molecule](https://github.com/erii-01/ansible-role-wordpress/actions/workflows/molecule.yml/badge.svg)](https://github.com/erii-01/ansible-role-wordpress/actions/workflows/molecule.yml)

# Rol de Ansible: WordPress

Un rol de Ansible para instalar y configurar un servidor web completo con WordPress y Apache. Es compatible con distribuciones de las familias Debian (Ubuntu) y Red Hat (Rocky Linux) y está probado con Molecule.

## Características

- Instala WordPress, Apache y las dependencias necesarias.
- Configura un Virtual Host para el sitio de WordPress.
- Multi-distribución: Lógica adaptativa para Debian/Ubuntu y RHEL/Rocky.
- Idempotente: Se puede ejecutar múltiples veces de forma segura.
- Genera el archivo `wp-config.php` con la configuración de la base de datos.
  > Para generar el wp-config.php se deben declarar las variables de la base de datos, tal como se indica en [Requerimientos](#requerimientos).

## Requisitos

Para probar este rol localmente, necesitas tener instalados:

- Git
- Docker (y asegurarse de que esté corriendo)
- [asdf](https://asdf-vm.com/)
- [direnv](https://direnv.net/)

## Entorno de Desarrollo

El proyecto utiliza asdf y direnv para automatizar la configuración del entorno, asegurando que todos usen las mismas versiones de las herramientas.

Clonar el repositorio:

```bash
git clone https://github.com/erii-01/ansible-role-wordpress.git
cd ansible-role-wordpress
```

Añadir los plugins de asdf (solo la primera vez):

```bash
asdf plugin add python
asdf plugin add ansible
```

Instalar las dependencias de Python:

```bash
pip install -r requirements.txt
```

Permitir a direnv activar el entorno:

```bash
direnv allow
```

## Requerimientos

Es necesario contar con un servidor de base de datos configurado con `db_name`, `db_user`, `db_password` y `db_host` accesibles para esta instancia de WordPress. Puede configurarlo en la misma máquina (por ejemplo, usando otro rol de Ansible como [geerlingguy.mysql](https://galaxy.ansible.com/geerlingguy/mysql/)), pero también puede ser una base de datos existente en otro host.

## Variables del Rol

| Variable          | Default                           | Comments                                    |
| :---------------- | :-------------------------------- | ------------------------------------------- |
| `site_domain`     | `"wordpress.local"`               | Dominio para el VirtualHost de Apache.      |
| `site_port`       | `"8081"`                          | Puerto del `host` para el `ServerAlias`.    |
| `wp_install_path` | `"/var/www/html/wordpress.local"` | Ruta de instalación de WordPress.           |
| `db_name`         | `"wordpress_db"`                  | Nombre de la base de datos de WordPress.    |
| `db_user`         | `"wordpress_user"`                | Usuario de la base de datos.                |
| `db_password`     | `"Pass12345"`                     | Contraseña del usuario de la base de datos. |
| `db_host`         | `"localhost"`                     | Host de la base de datos.                   |

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: webservers
  become: true
  roles:
    - role: erii-01.wordpress
```

## Pruebas

Este repositorio utiliza Molecule para las pruebas. Para ejecutar el ciclo completo de pruebas:

```bash
molecule test
```
