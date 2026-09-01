# Creador de Entornos Desechables LXC en Proxmox

Este repositorio proporciona un script automatizado en Bash para desplegar contenedores LXC (entornos desechables) en Proxmox VE de manera rápida y desatendida. Está diseñado para inicializar el contenedor, configurar sus recursos y red, e instalar automáticamente dependencias clave como `apt-fast` y un agente/runner (`precicd`) listo para integrarse a flujos de trabajo (como GitLab CI/CD).

## 🚀 Características

- **Despliegue automatizado:** Crea un contenedor LXC sin privilegios (`unprivileged: 1`) con soporte para anidamiento (`nesting=1` y `keyctl=1`).
- **Configuración centralizada:** Toda la parametrización (hardware, red, plantillas y tokens) se lee directamente desde un archivo `.env`.
- **Gestión inteligente de plantillas:** Verifica y descarga automáticamente la plantilla base de LXC si no se encuentra en la caché local.
- **Aprovisionamiento post-instalación:** Actualiza repositorios, añade el PPA `ppa:sinfallas/stuff`, instala y preconfigura `apt-fast` de manera no interactiva, e inicializa el servicio `precicd`.
- **Auto-registro de Runner:** Registra automáticamente el entorno en tu plataforma (ej. GitLab) usando los tokens y URLs definidos en la configuración.

## 📋 Requisitos Previos

- Un nodo con **Proxmox VE** en funcionamiento.
- Acceso SSH al host de Proxmox con privilegios de **root** (el script requiere ejecución como superusuario).
- Conexión a internet en el host Proxmox para descargar las plantillas de LXC.

## 🛠️ Instalación y Uso

1. **Clona el repositorio o descarga el script** en tu servidor Proxmox.
2. Modifica el archivo **desechable.env** para adaptarlo a sus necesidades.
3. **Otorga permisos de ejecución** al script:
```bash
chmod -v +x desechable
```
4. **Ejecuta el script de la siguiente forma:**
```bash
./desechable ./desechable.env
```
