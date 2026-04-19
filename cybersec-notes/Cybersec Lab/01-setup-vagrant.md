# Setup Vagrant + VirtualBox — Cybersec Lab

Date : 2025-04-19  
Statut : ✅ Opérationnel

---

## Stack installée
- VirtualBox : 7.0.22
- Vagrant : 2.4.9
- Git : 2.53.0
- Repo GitHub : `baldrExe/homelab`

---

## Installation sur nouveau poste Windows

```powershell
# 1. Installer Chocolatey
Set-ExecutionPolicy Bypass -Scope Process -Force
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# 2. Installer les outils — VirtualBox 7.0.22 OBLIGATOIRE (pas 7.2.x)
choco install virtualbox --version=7.0.22 vagrant git -y

# 3. PATH permanent VirtualBox
[System.Environment]::SetEnvironmentVariable(
  "PATH",
  $env:PATH + ";C:\Program Files\Oracle\VirtualBox",
  [System.EnvironmentVariableTarget]::Machine
)

# 4. Extension Pack — corrige le bug réseau Host-Only
mkdir C:\temp
Invoke-WebRequest -Uri "https://download.virtualbox.org/virtualbox/7.0.22/Oracle_VM_VirtualBox_Extension_Pack-7.0.22.vbox-extpack" -OutFile "C:\temp\Oracle_VM_VirtualBox_Extension_Pack-7.0.22.vbox-extpack"
vboxmanage extpack install "C:\temp\Oracle_VM_VirtualBox_Extension_Pack-7.0.22.vbox-extpack" --replace

# 5. REDÉMARRER WINDOWS avant de continuer
```

---

## Cloner et lancer le lab

```powershell
git clone https://github.com/baldrExe/homelab.git
cd homelab
vagrant up
```

---

## VMs et réseau

| VM | IP | Rôle |
|---|---|---|
| kali | 192.168.56.10 | Machine d'attaque |
| target (Ubuntu 22.04) | 192.168.56.20 | Cible lab |

- Réseau Host-Only isolé — VMs se voient entre elles, isolé du réseau domestique
- Test confirmé : ping 192.168.56.20 depuis Kali = ✅ 0% packet loss

---

## Fix réseau Host-Only si absent

```powershell
vboxmanage hostonlyif create
vboxmanage hostonlyif ipconfig "VirtualBox Host-Only Ethernet Adapter" --ip 192.168.56.1 --netmask 255.255.255.0
```

---

## Config IP permanente sur Ubuntu target

```bash
sudo nano /etc/netplan/01-netcfg.yaml
# Ajouter :
network:
  version: 2
  ethernets:
    enp0s8:
      addresses:
        - 192.168.56.20/24

sudo netplan apply
```

---

## Commandes Vagrant utiles

```powershell
vagrant up              # Démarrer toutes les VMs
vagrant up target       # Démarrer uniquement la cible
vagrant ssh kali        # SSH dans Kali
vagrant ssh target      # SSH dans la cible
vagrant halt            # Éteindre toutes les VMs
vagrant destroy --force # Supprimer toutes les VMs (Vagrantfile reste)
vagrant status          # État des VMs
```

---

## Problèmes rencontrés et solutions

| Problème | Cause | Solution |
|---|---|---|
| VBoxManage not found | PATH non configuré | Ajouter au PATH système + redémarrer PS |
| E_ACCESSDENIED | VirtualBox 7.2 incompatible Vagrant | Downgrader à 7.0.22 |
| VERR_INTNET_FLT_IF_NOT_FOUND | Adaptateur Host-Only absent | hostonlyif create + reboot Windows |

---

## Prochaine étape
- [[02-vulnhub-kioptrix1]]
