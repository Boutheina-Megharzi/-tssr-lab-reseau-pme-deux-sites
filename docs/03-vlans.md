# 03 – Création des VLAN

## Objectif
Je sépare les trois services du siège sur le switch `SW-L3` : Direction, Comptabilité et Informatique. Je crée un VLAN par service et j'affecte les ports des postes.

## Plan des VLAN
| VLAN | Nom | Ports de `SW-L3` | Poste |
|---|---|---|---|
| 10 | Direction | `Gig1/0/1`, `Gig1/0/4` | PC-DIR1, PC-DIR2 |
| 20 | Comptabilite | `Gig1/0/2` | PC-CPT |
| 30 | Informatique | `Gig1/0/3` | PC-INF |

Je n'écris pas d'accent dans les noms de VLAN pour éviter les problèmes d'affichage.

## Procédure

### 1. Ouvrir la CLI
J'ouvre la CLI de `SW-L3` (onglet **CLI**).

### 2. Nommer le switch
```
enable
configure terminal
hostname SW-L3
```

### 3. Créer les trois VLAN
```
vlan 10
name Direction
exit
vlan 20
name Comptabilite
exit
vlan 30
name Informatique
exit
```

### 4. Affecter les ports en mode accès
Exemple pour le port `Gig1/0/1` :
```
interface gigabitEthernet 1/0/1
switchport mode access
switchport access vlan 10
exit
```
Je répète pour `Gig1/0/4` (VLAN 10), `Gig1/0/2` (VLAN 20) et `Gig1/0/3` (VLAN 30).

### 5. Enregistrer la configuration
```
end
write memory
```
