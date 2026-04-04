# Splunk — Notes THM (SOC Level 1)

---

## Concepts SIEM

```
SIEM (Security Information & Event Management) :
  → Centralise les logs de toute l'infrastructure
  → Corrèle les événements pour détecter des attaques
  → Génère des alertes et permet l'investigation forensique

Sources de logs typiques :
  - Firewall              (trafic réseau, règles)
  - Windows Event Logs    (authentification, processus, services)
  - Web server logs       (requêtes HTTP)
  - Antivirus / EDR       (détections malware)
  - DNS logs              (requêtes de résolution)
```

## SPL — Splunk Processing Language

```spl
# Structure de base
index=main sourcetype=syslog
| stats count by host
| sort -count
| head 10

# Recherche par champ
index=main EventCode=4625           # Échecs de connexion Windows
index=main src_ip="192.168.1.100"

# Opérations courantes
| stats count by src_ip             # Compter par IP source
| sort -count                       # Trier décroissant
| table src_ip, dest_ip, action     # Afficher colonnes spécifiques
| where count > 100                 # Filtrer par valeur

# Recherche temporelle
earliest=-24h latest=now
earliest=-7d@d

# Détection brute force (exemple réel)
index=main EventCode=4625
| stats count by src_ip, user
| where count > 10
| sort -count
```

## Windows Event IDs à connaître

| Event ID | Description                            |
|----------|----------------------------------------|
| 4624     | Connexion réussie                      |
| 4625     | Échec de connexion                     |
| 4648     | Connexion avec credentials explicites  |
| 4672     | Privilèges spéciaux assignés           |
| 4688     | Création d'un nouveau processus        |
| 4698     | Tâche planifiée créée                  |
| 7045     | Nouveau service installé               |

## Ce que j'ai appris

- [ ] Compléter au fur et à mesure des rooms
