# Subnetting — Théorie et Exercices

## Formules à retenir

```
Hôtes utilisables  = 2^n - 2    (n = nombre de bits hôtes)
Sous-réseaux       = 2^s        (s = bits empruntés)
Incrément de bloc  = 256 - valeur du masque dans l'octet variable
```

## Tableau des masques courants

| Préfixe | Masque          | Hôtes utiles | Bloc |
|---------|-----------------|--------------|------|
| /24     | 255.255.255.0   | 254          | 256  |
| /25     | 255.255.255.128 | 126          | 128  |
| /26     | 255.255.255.192 | 62           | 64   |
| /27     | 255.255.255.224 | 30           | 32   |
| /28     | 255.255.255.240 | 14           | 16   |
| /29     | 255.255.255.248 | 6            | 8    |
| /30     | 255.255.255.252 | 2            | 4    |

## Méthode rapide — Exemple : 192.168.10.0/26

1. /26 → 2 bits empruntés dans le 4ème octet
2. Masque = 255.255.255.**192**
3. Bloc = 256 - 192 = **64**
4. Sous-réseaux : .0, .64, .128, .192
5. Pour 192.168.10.0/26 :
   - Réseau    : 192.168.10.**0**
   - 1er hôte : 192.168.10.**1**
   - Dernier   : 192.168.10.**62**
   - Broadcast : 192.168.10.**63**

## Exercices (sans calculatrice)

```
1. 172.16.0.0/20   → Combien d'hôtes ? Quel broadcast ?
2. 10.0.0.0/8      → Combien de /24 peut-on créer ?
3. 192.168.1.64/26 → Premier et dernier hôte ?
4. Besoin de 500 hôtes → Quel masque minimum ?
```

<details>
<summary>Réponses (cliquer pour révéler)</summary>

1. 4094 hôtes — broadcast 172.16.15.255
2. 65 536 sous-réseaux /24
3. Premier: .65 — Dernier: .126
4. /23 (510 hôtes utiles)

</details>

## Commandes

```bash
ipcalc 192.168.10.0/26    # Vérifier un subnet (Linux)
ip route show              # Table de routage Linux
route print                # Table de routage Windows
netstat -rn                # macOS / Linux
```
