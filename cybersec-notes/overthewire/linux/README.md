# Linux — Commandes essentielles

## Navigation et fichiers
```bash
pwd                          # Dossier actuel
ls -la                       # Lister avec permissions + fichiers cachés
cd /chemin                   # Changer de dossier
find / -name "*.txt"         # Chercher un fichier par nom
find / -perm -4000           # Fichiers SUID (clé pour la privesc)
grep -r "motclé" .           # Chercher du contenu récursivement
grep -i "motclé" fichier     # Insensible à la casse
grep -v "motclé" fichier     # Exclure les lignes qui matchent
cat fichier | grep "terme"   # Filtrer la sortie d'une commande
```

## Permissions
```bash
# Format : rwxrwxrwx  (owner | group | others)
# r=4  w=2  x=1

chmod 755 fichier            # rwxr-xr-x
chmod 644 fichier            # rw-r--r--
chmod +x script.sh           # Rendre exécutable
chown user:group fichier     # Changer le propriétaire

# SUID (chmod 4755) : s'exécute avec les droits du propriétaire
# Si owner = root + SUID → exécution en tant que root
```

## Processus
```bash
ps aux                       # Tous les processus
ps aux | grep nginx          # Filtrer par nom
kill -9 PID                  # Tuer un processus
systemctl status ssh         # Statut d'un service
```

## Réseau
```bash
ip addr show                 # Interfaces et IPs
ss -tuln                     # Ports en écoute
nc -lvnp 4444                # Netcat en écoute
```

## Chemins — règle importante
```bash
./fichier    # fichier dans le dossier actuel
/chemin      # chemin absolu depuis la racine
.            # dossier actuel et sous-dossiers (pour find)
/            # racine du système entier (pour find)
```