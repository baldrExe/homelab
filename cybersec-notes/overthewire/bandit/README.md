# Bandit — OverTheWire

Wargame Linux pour pratiquer les commandes de base.
Connexion : `ssh -p 2220 bandit0@bandit.labs.overthewire.org`
Mot de passe du level N = trouvé au level N-1.

---

## Level 0 → 1
**Objectif :** lire le fichier `readme` dans le home
```bash
cat readme
```

---

## Level 1 → 2
**Objectif :** lire un fichier nommé `-`
```bash
cat ./-
```

**Pourquoi `./-` ?**
Le `-` est interprété comme argument par le terminal.
`./` force la lecture comme fichier.

---

## Level 2 → 3
**Objectif :** lire un fichier avec des espaces dans le nom
```bash
cat "spaces in this filename"
# ou
cat spaces\ in\ this\ filename
# ou Tab pour autocomplétion
```

---

## Level 3 → 4
**Objectif :** lire un fichier caché
```bash
ls -la        # affiche les fichiers cachés (commençant par .)
cat .hidden
```

---

## Level 4 → 5
**Objectif :** trouver le seul fichier human-readable parmi plusieurs
```bash
file ./*      # détecte le type de chaque fichier
              # chercher "ASCII text"
cat ./-file07 # lire le bon fichier
```

**À retenir :** utiliser `file` avant `cat` quand on ne sait
pas quel fichier lire.

---

## Level 5 → 6
**Objectif :** fichier human-readable, 1033 bytes, non exécutable
```bash
find . -type f -size 1033c ! -executable
cat ./maybehere07/.file2
```

**Explications find :**
- `.`           → dossier actuel et sous-dossiers
- `-type f`     → fichiers uniquement
- `-size 1033c` → exactement 1033 bytes (c = bytes)
- `!`           → NOT, inverse la condition suivante
- `-executable` → fichier exécutable

---

## Level 6 → 7
**Objectif :** fichier somewhere on the server,
owned by bandit7, group bandit6, 33 bytes
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

**Explications :**
- `/`          → racine = tout le serveur
- `-user`      → appartient à cet utilisateur
- `-group`     → appartient à ce groupe
- `2>/dev/null`→ cache les erreurs "Permission denied"

**Règle chemin :**
- `./chemin` → chemin relatif (depuis où tu es)
- `/chemin`  → chemin absolu (depuis la racine, toujours)