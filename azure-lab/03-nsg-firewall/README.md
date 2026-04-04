# 03 — NSG & Firewall Rules

## Objectif
Configurer des Network Security Groups pour contrôler le trafic.
Comprendre NSG subnet vs NIC, et tester avec Network Watcher.

## Concepts clés à maîtriser

- NSG au niveau **subnet** vs NSG au niveau **NIC**
- Priorité des règles : plus le chiffre est bas = plus haute priorité
- Règles par défaut Azure : AllowVNetInBound, DenyAllInBound...
- **Inbound** (entrant) vs **Outbound** (sortant)

## Architecture cible

```
Internet
    │
    ▼ port 22 uniquement (depuis mon IP)
[NSG-public]
    │
    ▼
vm-linux (subnet-public)
    │
    ▼ port 3389 uniquement (RDP interne)
vm-windows (subnet-private)
[NSG-private] ← bloque tout trafic internet direct
```

## Étapes planifiées

1. Créer `nsg-public` et associer à subnet-public
2. Règle SSH (port 22) depuis mon IP uniquement
3. Créer `nsg-private` et associer à subnet-private
4. Bloquer tout trafic internet entrant sur subnet-private
5. Autoriser RDP (port 3389) depuis subnet-public uniquement
6. Vérifier avec Network Watcher > IP flow verify

## Ce que j'ai appris

- [ ] Compléter après la manipulation

## Erreurs rencontrées

- [ ] Documenter ici les problèmes et comment tu les as résolus

## Ressources

- [NSG overview](https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview)
- [Network Watcher](https://learn.microsoft.com/azure/network-watcher/)
