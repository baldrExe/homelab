# 02 — VM Deployment

## Objectif
Déployer deux VMs dans les subnets du lab 01 :
- VM Linux accessible en SSH (subnet public)
- VM Windows Server isolée (subnet privé, sans IP publique)

## Architecture

```
VNet : 10.0.0.0/16
├── Subnet-Public  : 10.0.1.0/24
│   └── vm-linux   (IP publique — SSH port 22)
└── Subnet-Private : 10.0.2.0/24
    └── vm-windows (pas d'IP publique)
```

## Prérequis

- Lab 01 terminé
- Clé SSH générée : `ssh-keygen -t rsa -b 4096 -C "azure-lab"`

## Commandes Azure CLI

```bash
# VM Linux dans subnet public
az vm create \
  --resource-group rg-lab-01 \
  --name vm-linux \
  --image Ubuntu2204 \
  --vnet-name vnet-lab \
  --subnet subnet-public \
  --admin-username azureuser \
  --ssh-key-values ~/.ssh/azure-lab.pub

# VM Windows dans subnet privé (sans IP publique)
az vm create \
  --resource-group rg-lab-01 \
  --name vm-windows \
  --image Win2022Datacenter \
  --vnet-name vnet-lab \
  --subnet subnet-private \
  --public-ip-address "" \
  --admin-username azureuser

# Connexion SSH à vm-linux
ssh -i ~/.ssh/azure-lab azureuser@<IP_PUBLIQUE_VM>
```

## Ce que j'ai appris

- [ ] Compléter après la manipulation

## Erreurs rencontrées

- [ ] Documenter ici les problèmes et comment tu les as résolus

## Ressources

- [Créer une VM Linux](https://learn.microsoft.com/azure/virtual-machines/linux/quick-create-cli)
- [Créer une VM Windows](https://learn.microsoft.com/azure/virtual-machines/windows/quick-create-cli)
