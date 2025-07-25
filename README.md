# Rol de Ansible: WordPress

Un rol de Ansible para instalar y configurar un servidor web completo con WordPress y Apache. Es compatible con distribuciones de las familias Debian (Ubuntu) y Red Hat (Rocky Linux) y está probado con Molecule.

## Características

- Instala WordPress, Apache y las dependencias necesarias.
- Configura un Virtual Host para el sitio de WordPress.
- Multi-distribución: Lógica adaptativa para Debian/Ubuntu y RHEL/Rocky.
- Idempotente: Se puede ejecutar múltiples veces de forma segura.

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

## Variables del Rol

Estas son las variables principales que se pueden modificar (ver `defaults/main.yml` para la lista completa):
| Variable | Descripción | Valor por Defecto |
| :---------------- | :----------------------------------------- | :------------------------------- |
| `wp_version` | La versión de WordPress a instalar. | `"6.5.5"` |
| `wp_install_path` | Ruta de instalación de WordPress. | `"/var/www/html/wordpress.local"`|
| `site_domain` | Dominio para el VirtualHost de Apache. | `"wordpress.local"` |
| `site_port` | Puerto del `host` para el `ServerAlias`. | `"8081"` |

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: webservers
  become: true
  roles:
    - role: erii-01.ansible_role_wordpress
```

## Pruebas

Este repositorio utiliza Molecule para las pruebas. Para ejecutar el ciclo completo de pruebas:

```bash
molecule test
```
