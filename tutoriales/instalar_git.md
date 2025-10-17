# Guía de Instalación de Git y Configuración con GitHub

## Windows

### Instalación de Git

1. Descarga Git desde [git-scm.com](https://git-scm.com/download/win)
2. Ejecuta el instalador descargado
3. Durante la instalación, acepta las opciones predeterminadas (son adecuadas para la mayoría de usuarios)
4. Verifica la instalación abriendo PowerShell o CMD y ejecutando:
   ```bash
   git --version
   ```

### Configuración de Credenciales

1. Abre Git Bash, PowerShell o CMD y configura tu nombre y correo:
   ```bash
   git config --global user.name "Tu Nombre"
   git config --global user.email "tuemail@ejemplo.com"
   ```

2. Configura Git Credential Manager (viene incluido con Git para Windows):
   ```bash
   git config --global credential.helper manager-core
   ```

3. La primera vez que intentes hacer push a GitHub, se abrirá una ventana para autenticarte con tu cuenta de GitHub.

---

## macOS

### Instalación de Git

**Opción 1: Usando Homebrew (recomendado)**
```bash
brew install git
```

**Opción 2: Usando Xcode Command Line Tools**
```bash
xcode-select --install
```

**Opción 3: Descarga el instalador** desde [git-scm.com](https://git-scm.com/download/mac)

Verifica la instalación:
```bash
git --version
```

### Configuración de Credenciales

1. Configura tu nombre y correo:
   ```bash
   git config --global user.name "Tu Nombre"
   git config --global user.email "tuemail@ejemplo.com"
   ```

2. Configura el Credential Helper de macOS:
   ```bash
   git config --global credential.helper osxkeychain
   ```

3. En el primer push a GitHub, se te pedirá autenticarte.

---

## Linux

### Instalación de Git

**Debian/Ubuntu:**
```bash
sudo apt update
sudo apt install git
```

**Fedora:**
```bash
sudo dnf install git
```

**Arch Linux:**
```bash
sudo pacman -S git
```

**CentOS/RHEL:**
```bash
sudo yum install git
```

Verifica la instalación:
```bash
git --version
```

### Configuración de Credenciales

1. Configura tu nombre y correo:
   ```bash
   git config --global user.name "Tu Nombre"
   git config --global user.email "tuemail@ejemplo.com"
   ```

2. Configura el almacenamiento de credenciales:
   ```bash
   git config --global credential.helper store
   ```
   O para mayor seguridad, usa cache (expira después de 15 minutos):
   ```bash
   git config --global credential.helper cache
   ```

---

## Autenticación con GitHub (Todos los Sistemas)

GitHub ya no acepta contraseñas para autenticación Git. Debes usar **Personal Access Tokens (PAT)** o **SSH**.

### Opción 1: Personal Access Token (PAT)

1. Ve a GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click en "Generate new token (classic)"
3. Dale un nombre descriptivo y selecciona los permisos necesarios (mínimo: `repo`)
4. Copia el token generado (¡no podrás verlo de nuevo!)
5. Cuando Git te pida contraseña, usa el PAT en lugar de tu contraseña de GitHub

### Opción 2: SSH (Recomendado)

1. Genera una clave SSH:
   ```bash
   ssh-keygen -t ed25519 -C "tuemail@ejemplo.com"
   ```
   Presiona Enter para aceptar la ubicación predeterminada.

2. Inicia el agente SSH:
   ```bash
   # Linux/macOS
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   
   # Windows (Git Bash)
   eval $(ssh-agent -s)
   ssh-add ~/.ssh/id_ed25519
   ```

3. Copia tu clave pública:
   ```bash
   # Linux/macOS
   cat ~/.ssh/id_ed25519.pub
   
   # Windows (PowerShell)
   type C:\Users\TuUsuario\.ssh\id_ed25519.pub
   ```

4. Agrega la clave a GitHub:
   - Ve a GitHub → Settings → SSH and GPG keys
   - Click "New SSH key"
   - Pega tu clave pública y guarda

5. Verifica la conexión:
   ```bash
   ssh -T git@github.com
   ```

### Verificar Configuración

Para ver tu configuración actual:
```bash
git config --list
```

¡Listo! Ya tienes Git instalado y configurado para trabajar con GitHub.