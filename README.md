# ParrotOS desktop enviroment.
Esta es una guía basada en [este](https://youtu.be/mHLwfI1nHHY) video de @s4vitar, no es con intención de hacer un plagio, es con intención de aprender y hacerle la vida un poquito más fácil a la gente.

[Aquí](https://pastebin.com/EEX1Dsuq) está el pastebin original.

### 1. Actualizamos el sistema.
```bash
sudo apt upgrade```
Esto lleva un rato...
### 2. Clonamos este repositorio.
```bash
cd ~/Descargas/
```
```bash
git clone https://github.com/amorinn/ParrotOS-desktop-enviroment.git
```
### 3. Instalamos los siguientes paquetes:
```bash
sudo apt install build-essential git vim xcb libxcb-util0-dev libxcb-ewmh-dev libxcb-randr0-dev libxcb-icccm4-dev libxcb-keysyms1-dev libxcb-xinerama0-dev libasound2-dev libxcb-xtest0-dev libxcb-shape0-dev 
```
### 4. Instalamos bspwm y sxhkd:
```bash
cd ~/Descargas/
```
```bash
git clone https://github.com/baskerville/bspwm.git
```
```bash
git clone https://github.com/baskerville/sxhkd.git
```
```bash
cd bspwm/
```
```bash
make
```
```bash
sudo make install
```
```bash
cd ../sxhkd/
```
```bash
make
```
```bash
sudo make install
```
```bash
sudo apt install bspwm
```
### 5. Cargamos en bspwm y sxhkd ficheros de ejemplo:
```bash
mkdir ~/.config/bspwm
```
```bash
mkdir ~/.config/sxhkd
```
```bash
cd /home/s4vitar/Descargas/bspwm/
```
```bash
cp examples/bspwmrc ~/.config/bspwm/
```
```bash
chmod +x ~/.config/bspwm/bspwmrc 
```
```bash
cp examples/sxhkdrc ~/.config/sxhkd/
```
### 6. Añadimos keybindings a sxhkd:
Modificamos `~/.config/sxhkd/sxhkdrc` borramos su contenido y pegamos los siguiente:
```# ------------------------------------------------------------------------------------------------
#
# wm independent hotkeys
#
 
# terminal emulator
super + Return
    gnome-terminal
 
# program launcher
super + d
    rofi -show run
 
# make sxhkd reload its configuration files:
super + Escape
    pkill -USR1 -x sxhkd
 
#
# bspwm hotkeys
#
 
# quit/restart bspwm
super + alt + {q,r}
    bspc {quit,wm -r}
 
# close and kill
super + {_,shift + }w
    bspc node -{c,k}
 
# alternate between the tiled and monocle layout
super + m
    bspc desktop -l next
 
# send the newest marked node to the newest preselected node
super + y
    bspc node newest.marked.local -n newest.!automatic.local
 
# swap the current node and the biggest node
super + g
    bspc node -s biggest
 
#
# state/flags
#
 
# set the window state
super + {t,shift + t,s,f}
    bspc node -t {tiled,pseudo_tiled,floating,fullscreen}
 
# set the node flags
super + ctrl + {m,x,y,z}
    bspc node -g {marked,locked,sticky,private}
 
#
# focus/swap
#
 
super + {_,shift + }{Left,Down,Up,Right}
       bspc node -{f,s} {west,south,north,east}
 
 
# focus the node for the given path jump
super + {p,b,comma,period}
    bspc node -f @{parent,brother,first,second}
 
# focus the next/previous node in the current desktop
super + {_,shift + }c
    bspc node -f {next,prev}.local
 
# focus the next/previous desktop in the current monitor
super + bracket{left,right}
    bspc desktop -f {prev,next}.local
 
# focus the last node/desktop
super + {grave,Tab}
    bspc {node,desktop} -f last
 
# focus the older or newer node in the focus history
super + {o,i}
    bspc wm -h off; \
    bspc node {older,newer} -f; \
    bspc wm -h on
 
# focus or send to the given desktop
super + {_,shift + }{1-9,0}
    bspc {desktop -f,node -d} '^{1-9,10}'
 
#
# preselect
#
 
# preselect the direction
super + ctrl + alt + {Left,Down,Up,Right}
    bspc node -p {west,south,north,east}
 
 
# preselect the ratio
super + ctrl + {1-9}
    bspc node -o 0.{1-9}
 
# cancel the preselection for the focused node
super + ctrl + space
    bspc node -p cancel
 
# cancel the preselection for the focused desktop
super + ctrl + alt + space
    bspc query -N -d | xargs -I id -n 1 bspc node id -p cancel
 
#
# move/resize
#
 
# expand a window by moving one of its side outward
#super + alt + {h,j,k,l}
#   bspc node -z {left -20 0,bottom 0 20,top 0 -20,right 20 0}
 
# contract a window by moving one of its side inward
#super + alt + shift + {h,j,k,l}
#   bspc node -z {right -20 0,top 0 20,bottom 0 -20,left 20 0}
 
# move a floating window
super + ctrl + {Left,Down,Up,Right}
    bspc node -v {-20 0,0 20,0 -20,20 0}
 
# Custom move/resize
alt + super + {Left,Down,Up,Right}
    ~/.config/bspwm/scripts/bspwm_resize {west,south,north,east}
# ------------------------------------------------------------------------------------------------```
Y ejecutamos:
```bash
mkdir ~/.config/bspwm/scripts/
```
```bash
cp ~/Descargas/ParrotOS-desktop-enviroment ~/.config/bspwm/scripts
```
```bash
chmod +x ~/.config/bspwm/scripts/bspwm_resize
```

### 7. Procedemos a instalar la polybar.
Para ello instalamos los siguientes paquetes:
```bash
sudo apt install cmake cmake-data pkg-config python3-sphinx libcairo2-dev libxcb1-dev libxcb-util0-dev libxcb-randr0-dev libxcb-composite0-dev python3-xcbgen xcb-proto libxcb-image0-dev libxcb-ewmh-dev libxcb-icccm4-dev libxcb-xkb-dev libxcb-xrm-dev libxcb-cursor-dev libasound2-dev libpulse-dev libjsoncpp-dev libmpdclient-dev libcurl4-openssl-dev libnl-genl-3-dev livub1-dev
```
Para instalar la polybar hacemos lo siguiente:
```bash
cd ~/Descargas/
```
```bash
git clone --recursive https://github.com/polybar/polybar
```
```bash
cd polybar/
```
```bash
mkdir build
```
```bash
cd build/
```
```bash
cmake ..
```
```bash
make -j$(nproc)
```
```bash 
sudo make install
```
### 8. Procedemos con la instalación de Picom
Actualizamos el sistema:
```bash
sudo apt update
```
E instalamos los siguientes paquetes:
```bash
sudo apt install meson libxext-dev libxcb1-dev libxcb-damage0-dev libxcb-xfixes0-dev libxcb-shape0-dev libxcb-render-util0-dev libxcb-render0-dev libxcb-randr0-dev libxcb-composite0-dev libxcb-image0-dev libxcb-present-dev libxcb-xinerama0-dev libpixman-1-dev libdbus-1-dev libconfig-dev libgl1-mesa-dev libpcre2-dev libevdev-dev uthash-dev libev-dev libx11-xcb-dev libxcb-glx0-dev feh rofi
```
A continuación
```bash
cd ~/Descargas/
```
```bash
git clone https://github.com/ibhagwan/picom.git
```
```bash
cd picom/
```
```bash
git submodule update --init --recursive
```
```bash
meson --buildtype=release . build
```
```bash
ninja -C build
```
```bash
sudo ninja -C build install
```
### 9. Reiniciamos y seleccionamos bspwm
Para seleccionar **bspwm** clickamos encima del circulo blanco que nos aparece en la derecha de nuestro usuario en la pantalla de bloqueo cuando reiniciamos y seleccionamos bspwm y nos logueamos.
>Si no quieres reiniciar haz ```kill -9 -1 ```.

Una vez dentro se verá todo en negro, al pulsar **super + enter** se nos abrirá una terminal.
> Siendo "super" la tecla de windows

### 10. Instalamos la Hack Nerd Font.
Ejecutamos los siguientes comandos:
```bash
cd ~/Descargas/
```
```bash
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/Hack.zip
```
```bash
sudo mv  ~/Descargas/Hack.zip /usr/local/share/fonts
```
```bash
cd /usr/local/share/fonts
```
```bash
unzip Hack.zip
```
```bash
sudo rm Hack.zip
```
```bash
fc-cache -v
```
y ya tendríamos las Hack Nerd fonts instaladas, ahora nos dirigimos al apartado "Editar" en una terminal y elegimos perfiles, desmarcamos la casilla de "Usar la tipografía de ancho fijo del sistema" y seleccionamos "Hack nerd fonts mono regular". Antes de salir desmarcamos las casillas de "Permitir texto resaltado","Mostrar la barra de menús en los terminales nuevos por defecto" y "Campana del terminal". Y por último vamos a la pestaña de desplazamiento y donde dice "La barra de desplazamiento está:" seleccionamos desconectado.

### 11. Configuramos un fondo de pantalla:
​Descargamos el fondo y lo movemos al directorio que queramos. 
```bash
echo "feh --bg-fill /ruta/al/fondo.jpg" >> ~/.config/bspwm/bspwmrc
```
> Siendo "/ruta/al/fondo" la ruta a nuestro fondo.
> Si quieres puedes utilizar el que ya viene en ~/Descargas/ParrotOS-desktop-enviroment.

### 12. Configuramos la polybar.
```bash
cd ~/Descargas
git clone https://github.com/VaughnValle/blue-sky.git
```
```bash
mkdir ~/.config/polybar
```
```bash
cd ~/Descargas/blue-sky/polybar/
```
```bash
cp * -r ~/.config/polybar
```
```bash
echo '~/.config/polybar/./launch.sh' >> ~/.config/bspwm/bspwmrc
```
```bash
cd fonts
sudo cp * /usr/share/fonts/truetype/
```
```
fc-cache -v
```
Pulsamos **super + r** para ver la polybar.
> [Aquí](https://github.com/PrayagS/polybar-spotify) puedes aprender a hacer un módulo para spotify.

### 13. Configuramos picom.
```bash
mkdir ~/.config/picom
cd ~/.config/picom
```
```bash
cp ~/Descargas/blue-sky/picom.conf .
```
Luego modificamos picom.conf y comentamos 'backend ="glx"' y descomentamos 'backend = "xrender"' ​

Antes de recargar la configuración, hacemos un seguimiento del ratón para saber en qué ventana estamos con el siguiente comando:
​
```bash
echo "bspc config focus_follows_pointer true" >> ~/.config/bspwm/bspwmrc
```
Posteriormente, ejecutamos los siguientes comandos para aplicar los bordeados:
```bash
echo 'picom --experimental-backends &' >> ~/.config/bspwm/bspwmrc 
```
```bash
echo 'bspc config border_width 0' >> ~/.config/bspwm/bspwmrc
```
Y hacemos **super + r** para ver los cambios.
>Si experimentamos lentitud o problemas de rendimiento probamos a volver a descomentar 'backend = "glx"' y a comentar 'backend = "xrender"' en ~/.config/picom/picom.comf y si eso no funciona jugamos con los ajustes de picom.comf

### 14. Instalamos el tema nord para rofi.
En una terminal escribimos ```rofi-theme-selector``` y se nos abrirá rofi con un a selección de temas para elegir, abajo de todo estará el tema nord, ponemos el seleccionador encima y pulsamos **alt + a**.

### 15. Configuramos la polybar. 
Ejecutamos:
```bash
echo "xsetroot -cursor_name left_ptr &" >> ~/.config/bspwm/bspwmrc
```
Para configurar el estilo de la polybar editamos ***~/.config/polybar/current.ini*** y modificamos todo a nuestro antojo.
### 16. Instalamos Slim y Slimlock.
```bash
sudo apt update
```
```bash
sudo apt install slim libpam0g-dev libxrandr-dev libfreetype6-dev libimlib2-dev libxft-dev​
```
```bash
cd ~/Descargas/
```
```bash
git clone https://github.com/joelburget/slimlock.git
```
```bash
cd slimlock/
```

```bash
sudo make
```
```bash
sudo make install
```
```bash
cd ~/Descargas/blue-sky/slim
```
```bash
sudo cp slim.conf /etc/
```
```bash
sudo cp slimlock.conf /etc
```
```bash
cd ~/Descargas
```
```bash
git clone https://github.com/adi1090x/slim_themes.git
```
```bash
cd /slim-themes/themes
```
```bash
mv /overlay /default
```
```bash
sudo cp -r  default /usr/share/slim/themes
```
Y reiniciamos el equipo.
###  17. Instalamos la powerlevel10k.
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc 
```
Despues escribimos ```zsh``` y empezará la configuración de la powerlevel10k, elegimos las opciones que mas se adapten a nosotros. Y lo volvemos a hacer con el usuario **Root**.
Ahora tendremos que hacer que la zsh sea nuestra shell predeterminada con estos dos comandos:
```bash
usermod --shell /usr/bin/zsh tuUsuario 
```
>Donde pone "tuUsuario" pones tu usuario :neutral_face:.

```bash
usermod --shell /usr/bin/zsh root
```
Y enlazamos el .zshrc de nuestro usuario con el de Root:
```bash
sudo ln -s -f ~/.zshrc /root/.zshrc 
```
Luego editamos el archivo .p10k a nuestro gustos y con nuestros propios colores.
Para arreglar un problema de permisos al migrar de su a nuestro usuario ejecutamos los siguientes comandos.
```bash
chown tuUsuario:tuUsuario /root
```
```bash
chown tuUsuario:tuUsuario /root/.cache -R
```
```bash
chown tuUsuario:tuUsuario /root/.local -R
```
### 18. Instalamos bat, lsd, fzf y ranger.
```bash
cd ~/Descargas/
```
```bash
wget https://github.com/Peltoche/lsd/releases/download/0.20.1/lsd_0.20.1_amd64.deb
```
```bash
wget https://github.com/sharkdp/bat/releases/download/v0.18.3/bat_0.18.3_amd64.deb
```
```bash
sudo dpkg -i *.deb
```
```bash
sudo apt install fzf ranger
```
### 19. Instalamos plugins para la zsh.
```bash
cd /usr/share
```
```bash
sudo mkdir zsh-plugins
```
```bash
sudo chown tuUsuario:tuUsuario zsh-plugins
```
```bash
cd zsh-plugins
```
```bash
wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/plugins/sudo/sudo.plugin.zsh
```
### 20. Configuramos los aliases.
```bash
cd ~/Descargas/ParrotOS-desktop-enviroment
```
```bash
cat aliases >> ~/.zshrc
```

## Resultados.
![1](https://user-images.githubusercontent.com/83926750/144131700-9fdf4bfd-c6be-4890-8c1c-829981b38654.jpg)
![3](https://user-images.githubusercontent.com/83926750/144131787-689a4792-3918-486d-9135-b609b0273067.jpg)

