# Active Directory — Notes THM

Room : Active Directory Basics

---

## Concepts fondamentaux

```
Domaine            : unité d'administration centrale (ex: company.local)
Domain Controller  : serveur qui gère le domaine (LDAP, Kerberos, DNS)
Forest             : ensemble de domaines liés par des trusts
OU (Org Unit)      : conteneur logique pour organiser les objets AD
GPO (Group Policy) : politiques appliquées aux OUs

Objets principaux :
  Users     → comptes utilisateurs
  Groups    → groupes de sécurité ou distribution
  Computers → machines jointes au domaine
```

## Authentification Kerberos (simplifié)

```
1. User → DC   : "Je veux me connecter"                    (AS-REQ)
2. DC   → User : Ticket TGT chiffré avec hash password     (AS-REP)
3. User → DC   : "J'ai besoin d'accéder à un service"      (TGS-REQ + TGT)
4. DC   → User : Ticket de service (TGS)                   (TGS-REP)
5. User → Svc  : "Voilà mon ticket"                        (AP-REQ)
```

> Attaques courantes sur Kerberos : Kerberoasting, Pass-the-Hash,
> AS-REP Roasting, Golden Ticket — voir rooms THM dédiées.

## Commandes d'énumération (Windows)

```powershell
# Users et groupes
net user                              # Users locaux
net user /domain                      # Users du domaine
net group /domain                     # Groupes du domaine
net group "Domain Admins" /domain     # Membres d'un groupe spécifique

# PowerShell AD (si module disponible)
Get-ADUser -Filter * -Properties *
Get-ADGroup -Filter *
Get-ADComputer -Filter *
Get-ADGroupMember "Domain Admins"
```

## Ce que j'ai appris

- [ ] Compléter au fur et à mesure des rooms
