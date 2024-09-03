# Guía de Configuración de Fedora


## Tabla de Contenidos
1. [Configurar DNF para Descargas más Rápidas](#configurar-dnf-para-descargas-más-rápidas)
   - [Editar la Configuración de DNF](#editar-la-configuración-de-dnf)
2. [Actualizar el Sistema](#actualizar-el-sistema)
   - [Actualizar y Mejorar el Sistema](#actualizar-y-mejorar-el-sistema)
3. [Habilitar RPM Fusion y Otros Repositorios de Terceros](#habilitar-rpm-fusion-y-otros-repositorios-de-terceros)
   - [Instalar RPM Fusion](#instalar-rpm-fusion)
   - [Instalar Gnome Tweaks y la Aplicación de Extensiones](#instalar-gnome-tweaks-y-la-aplicación-de-extensiones)
4. [Configuración de Multimedia en Fedora](#configuración-de-multimedia-en-fedora)
   - [Cambiar a ffmpeg completo](#cambiar-a-ffmpeg-completo)
   - [Instalar Codecs Adicionales](#instalar-codecs-adicionales)
   - [Codecs Acelerados por Hardware](#codecs-acelerados-por-hardware)
5. [Instalar Controladores NVIDIA](#instalar-controladores-nvidia)
   - [Instalación de los Controladores](#instalación-de-los-controladores)
   - [(Opcional) Instala soporte para CUDA/NVDEC/NVENC](#opcional-instala-soporte-para-cudanvdecnvenc)
6. [Instalación del Tema Nordic](#instalación-del-tema-nordic)
   - [Aplicar el tema en Gnome](#aplicar-el-tema-en-gnome)
   - [Configurar GTK 4.0](#configurar-gtk-40)
7. [Instalación de Extensiones para Gnome](#instalación-de-extensiones-para-gnome)
   - [Extensiones del Usuario](#extensiones-del-usuario)
   - [Instalación de Extensiones](#instalación-de-extensiones)

## Configurar DNF para Descargas más Rápidas


### Editar la Configuración de DNF


1. Abre una terminal.
2. Edita el archivo de configuración de DNF ubicado en `/etc/dnf/dnf.conf` con el siguiente comando:

    ```bash
    sudo nano /etc/dnf/dnf.conf
    ```

3. Añade la siguiente línea al archivo para aumentar el número de descargas paralelas:

    ```
    max_parallel_downloads=10
    ```

4. Guarda y cierra el archivo.


## Actualizar el Sistema


### Actualizar y Mejorar el Sistema


1. Abre una terminal.
2. Ejecuta el siguiente comando para actualizar el sistema:

    ```bash
    sudo dnf update
    ```

3. Luego, ejecuta este comando para aplicar las mejoras y actualizaciones disponibles:

    ```bash
    sudo dnf upgrade
    ```


## Habilitar RPM Fusion y Otros Repositorios de Terceros


### Instalar RPM Fusion

1. Abre una terminal.
2. Ejecuta los siguientes comandos para habilitar los repositorios de RPM Fusion (libres y no libres):

    ```bash
    sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
    ```

    ```bash
    sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
    ```

### Instalar Gnome Tweaks y la Aplicación de Extensiones

```bash
sudo dnf install gnome-tweaks gnome-extensions-app
```

## Configuración de Multimedia en Fedora


### Cambiar a ffmpeg completo

El `ffmpeg-free` de Fedora funciona la mayor parte del tiempo, pero puede haber problemas de compatibilidad de versiones. Para obtener una mejor compatibilidad, se recomienda cambiar a la versión completa de `ffmpeg` proporcionada por RPM Fusion:

```bash
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
```

## Instalar Codecs Adicionales


```bash

sudo dnf update @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
```


```bash
sudo dnf update @sound-and-video
```

### Codecs Acelerados por Hardware


```bash
sudo dnf install libva-nvidia-driver
```
## Instalar Controladores NVIDIA


```bash
sudo dnf update -y
```

Luego, reinicia el sistema 

Instalar el módulo akmod-nvidia para obtener los controladores NVIDIA:

```bash

sudo dnf install akmod-nvidia
```

### (Opcional) Instala soporte para CUDA/NVDEC/NVENC:

```bash

sudo dnf install xorg-x11-drv-nvidia-cuda
```


Para verificar que el módulo se haya construido correctamente

```bash

modinfo -F version nvidia
```
Debería devolver la versión del controlador, y no un error de módulo no encontrado.


## Instalación del Tema Nordic theme

1. **Descarga y extrae el archivo ZIP del tema:**
   - Descarga el archivo ZIP del repositorio [Nordic](https://github.com/EliverLara/Nordic).
   - Extrae el archivo ZIP en el directorio de temas, es decir, `/usr/share/themes/` o `~/.themes/` (crea el directorio si es necesario).

2. **Aplicar el tema en Gnome:**

   Para establecer el tema en Gnome, ejecutar los siguientes comandos en la Terminal:

   ```bash
   gsettings set org.gnome.desktop.interface gtk-theme "Nordic"
   gsettings set org.gnome.desktop.wm.preferences theme "Nordic"
   ```

3. **Configurar GTK 4.0:**

Copiar el contenido de la carpeta ~/.themes/Nordic/gtk-4.0/ y llévalo a ~/.config/gtk-4.0/, incluyendo la carpeta assets para que se apliquen correctamente los botones y otros elementos gráficos.

![image](https://github.com/user-attachments/assets/be8a1c1a-8e31-4bb1-a907-292ba121bb89)

## Instalación de Extensiones para Gnome

### Extensiones del Usuario

1. **AppIndicator and KStatusNotifierItem Support**
   - Esta extensión permite el soporte para indicadores de aplicaciones en la barra superior de Gnome.

2. **ArcMenu**
   - Agrega un menú de aplicaciones estilo "Arc" en Gnome.

3. **Blur my Shell**
   - Añade un efecto de desenfoque en el fondo del shell de Gnome.

4. **Dash to Dock**
   - Convierte el dash de Gnome en un dock personalizable.

5. **Desktop Icons NG (DING)**
   - Permite mostrar iconos en el escritorio.

6. **Hide Top Bar**
   - Oculta la barra superior de Gnome automáticamente cuando no está en uso.

7. **[QSTweak] Quick Setting Tweaker**
   - Permite ajustar configuraciones rápidas desde el shell de Gnome.

8. **Rounded Window Corners Reborn**
   - Añade esquinas redondeadas a las ventanas en Gnome.

9. **User Themes**
   - Habilita la opción de seleccionar temas de usuario desde la configuración de Gnome.


### Instalación de Extensiones

Para instalar estas extensiones, sigue estos pasos:

1. **Instalar Gnome Extensions App:**

    ```bash
    sudo dnf install gnome-extensions-app
    ```

2. **Buscar e instalar las extensiones desde la [página de Gnome Extensions](https://extensions.gnome.org/) o utilizando la Gnome Extensions App.**

3. **Activar las extensiones utilizando la aplicación `Gnome Tweaks` o la aplicación `Gnome Extensions` instalada previamente.**

Una vez que hayas instalado y activado estas extensiones, tu entorno de escritorio Gnome debería estar configurado de acuerdo a las preferencias vistas en la imagen.
