# Bandit — OverTheWire

Wargame Linux pour pratiquer les commandes de base.
Connexion : `ssh -p 2220 banditN@bandit.labs.overthewire.org`
Mot de passe du level N = trouvé au level N-1.

---

## Level 0 → 1
```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
cat readme
# password : ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

---

## Level 1 → 2
```bash
ssh -p 2220 bandit1@bandit.labs.overthewire.org
cat < -
# password : 263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

**Pourquoi `< -` ?**
Le `-` est interprété comme argument par le terminal.
La redirection `<` force la lecture comme fichier.

---

## Level 2 → 3
```bash
ssh -p 2220 bandit2@bandit.labs.overthewire.org
cat "spaces in this filename"
# password : MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

**À retenir :** guillemets autour des noms avec espaces.

---

## Level 3 → 4
```bash
ssh -p 2220 bandit3@bandit.labs.overthewire.org
ls -la inhere/
cat inhere/...Hiding-From-You
# password : 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

**À retenir :** `ls -la` pour voir les fichiers cachés (commençant par `.`).

---

## Level 4 → 5
```bash
ssh -p 2220 bandit4@bandit.labs.overthewire.org
file ./*
cat ./-file07
# password : 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

**À retenir :** `file` avant `cat` pour identifier le type de fichier.

---

## Level 5 → 6
```bash
ssh -p 2220 bandit5@bandit.labs.overthewire.org
find . -type f -size 1033c ! -executable
cat ./maybehere07/.file2
# password : HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

**Explications find :**
- `.`            → dossier actuel et sous-dossiers
- `-type f`      → fichiers uniquement
- `-size 1033c`  → exactement 1033 bytes (c = bytes)
- `!`            → NOT, inverse la condition suivante
- `-executable`  → fichier exécutable

---

## Level 6 → 7
```bash
ssh -p 2220 bandit6@bandit.labs.overthewire.org
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
# password : morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

**Explications :**
- `/`            → racine = tout le serveur
- `-user`        → appartient à cet utilisateur
- `-group`       → appartient à ce groupe
- `2>/dev/null`  → cache les erreurs Permission denied

---

## Level 7 → 8
```bash
ssh -p 2220 bandit7@bandit.labs.overthewire.org
grep "millionth" data.txt
# password : dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

**À retenir :** `grep "mot" fichier` pour trouver une ligne contenant un mot précis.

---

## Level 8 → 9
```bash
ssh -p 2220 bandit8@bandit.labs.overthewire.org
sort data.txt | uniq -u
# password : 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

**Explications :**
- `sort`         → trie les lignes (doublons côte à côte)
- `|`            → pipe, envoie la sortie vers la commande suivante
- `uniq -u`      → affiche uniquement les lignes uniques (1 seule occurrence)

**À retenir :** `uniq` ne fonctionne que sur des lignes adjacentes →
toujours `sort` avant `uniq`.

---

## Level 9 → 10
```bash
ssh -p 2220 bandit9@bandit.labs.overthewire.org
strings data.txt | grep =
# password : FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

À retenir : `strings` extrait les séquences de caractères lisibles d'un fichier binaire/mixte. Combiner avec `grep` pour filtrer sur un pattern précis.

---

## Level 10 → 11
``` bash
ssh -p 2220 bandit10@bandit.labs.overthewire.org
base64 -d data.txt
# password : dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

À retenir :
* `base64` → encode du binaire en texte pur (lettres + chiffres + `+/=`)
* `-d` → **décoder** — sans cette option, la commande **encode** par défaut

---

## Level 11 → 12
```bash
ssh -p 2220 bandit11@bandit.labs.overthewire.org
cat data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'
# password : 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

À retenir :
* `tr 'SET1' 'SET2'` → remplace chaque caractère de SET1 par le caractère à la même position dans SET2
* Les deux sets doivent avoir la **même longueur**
* ROT13 = décalage de 13 positions → `a-z` devient `n-za-m` (13+13 pour boucler l'alphabet)
---

## Level 12 → 13
```bash
ssh -p 2220 bandit12@bandit.labs.overthewire.org
mktemp -d
cp ~/data.txt /tmp/tmp.isaSv3LKv9/
cd /tmp/tmp.isaSv3LKv9
xxd -r data.txt > data2
# Répéter : file → renommer → décompresser jusqu'à ASCII text
mv data2 data2.gz && gzip -d data2.gz
mv data2 data2.bz2 && bzip2 -d data2.bz2
tar -xf data2
tar -xf data5.bin
mv data6.bin data6.bz2 && bzip2 -d data6.bz2
tar -xf data6
mv data8.bin data8.gz && gzip -d data8.gz
cat data8
# password : FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

```

À retenir :
* `xxd -r` → convertit un hexdump en binaire
* `file` → à utiliser à chaque étape pour identifier le type de compression
* `gzip -d` / `bzip2 -d` → décompresser (sans `-d` = compresse)
* `tar -xf` → extrait une archive tar
* Les outils de compression sont souvent **chaînés** — toujours `file` après chaque décompression
