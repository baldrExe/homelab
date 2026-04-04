# Azure Lab — Pratique AZ-900 / AZ-104

Lab personnel pour apprendre et documenter mes déploiements Azure,
en parallèle de la préparation aux certifications AZ-900 et AZ-104.

## Progression

| Projet | Statut | Concepts couverts |
|--------|--------|-------------------|
| [01 — VNet Basics](./01-vnet-basics/) | ✅ Terminé | VNet, Subnets, Adressage IP |
| [02 — VM Deployment](./02-vm-deployment/) | 🔄 En cours | VM, IP publique, SSH |
| [03 — NSG & Firewall](./03-nsg-firewall/) | ⏳ Planifié | NSG, règles inbound/outbound |

## Stack utilisée

- Azure Portal
- Azure CLI
- Draw.io (schémas)
- Terraform *(à venir)*

## Compte Azure

Compte gratuit (200 USD de crédits) — aucune donnée sensible dans ce repo.
Toutes les clés et credentials sont dans `.env` (ignoré par git).

## Objectif final

Être capable de déployer une infrastructure réseau complète
(VNet, subnets, VMs, NSG, Load Balancer) sans documentation,
et de l'automatiser avec Terraform.
