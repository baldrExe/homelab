# 01 — VNet Basics

## Objectif
Déployer un réseau virtuel Azure avec deux subnets (public et privé)
et comprendre l'adressage IP dans Azure.

## Architecture

```
VNet : 10.0.0.0/16
├── Subnet-Public  : 10.0.1.0/24
└── Subnet-Private : 10.0.2.0/24
```

## Étapes réalisées

1. Créer un Resource Group `rg-lab-01`
2. Déployer un VNet `vnet-lab` avec l'espace `10.0.0.0/16`
3. Créer le subnet public `10.0.1.0/24`
4. Créer le subnet privé `10.0.2.0/24`

## Commandes Azure CLI

```bash
az group create --name rg-lab-01 --location switzerlandnorth

az network vnet create \
  --resource-group rg-lab-01 \
  --name vnet-lab \
  --address-prefix 10.0.0.0/16

az network vnet subnet create \
  --resource-group rg-lab-01 \
  --vnet-name vnet-lab \
  --name subnet-public \
  --address-prefix 10.0.1.0/24

az network vnet subnet create \
  --resource-group rg-lab-01 \
  --vnet-name vnet-lab \
  --name subnet-private \
  --address-prefix 10.0.2.0/24
```

## Ce que j'ai appris

- [ ] Compléter après la manipulation

## Erreurs rencontrées

- [ ] Documenter ici les problèmes et comment tu les as résolus

## Ressources

- [VNet overview](https://learn.microsoft.com/azure/virtual-network/virtual-networks-overview)
- [Gérer les subnets](https://learn.microsoft.com/azure/virtual-network/virtual-network-manage-subnet)
