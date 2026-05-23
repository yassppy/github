### 🛠️ Versión
`git --version`                 # Obtener la versión de git

### Instalación Mac, Linux y Microsoft

`brew install git`                 # Para instalar en Mac
`sudo apt install git-all`                 # Para instalar en Linux
`sudo dfn install git-all`                 # Para instalar en Linux
Para Windows https://git-scm.com/install/windows

### Configuración inicial

```
git config --global user.name "miguelmallquidiaz"
git config --global user.email "correo"
git config --global user.password token-generado
```
### Error de credenciales debido a que tengo otra cuenta en uso

- Primero se debe buscar el administrador de credenciales y dirigirnos a la opción de "Credenciales de Windows" y quitar la cuenta que ya no quiero.

`git config --list`    # Nos permite ver todo la configuración inicial y salimos con `q`

### Configuración de la llave SSH
Es una llave compartida entre nuestro computador y GitHub que permite conectarse a través del protocolo SSH.
