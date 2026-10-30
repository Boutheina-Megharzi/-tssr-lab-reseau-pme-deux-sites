# tssr-lab-reseau-pme-deux-sites

Laboratoire réseau Cisco Packet Tracer : topologie, VLAN, routage entre VLAN, routage statique entre deux sites, DHCP et tests de connectivité.

## Contexte (scénario fictif)
Une PME fictive a son siège à Lyon et une agence à Grenoble. Le siège compte trois services (Direction, Comptabilité, Informatique), chacun dans son VLAN. L'agence a son propre réseau. Je conçois, je construis, je configure et je teste ce réseau.

## Objectif
Je relie le siège et l'agence, je sépare les services du siège avec des VLAN, je configure le routage et le DHCP, puis je teste la communication de poste à poste.

## Environnement
- Cisco Packet Tracer 9.0.1.0858
- 2 routeurs (2911), 2 switchs (3650-24PS et 2960-24TT), 5 postes

## Plan d'adressage
| Réseau | VLAN | Adresse | Passerelle |
|---|---|---|---|
| Direction | 10 | `192.168.10.0/24` | `192.168.10.1` |
| Comptabilité | 20 | `192.168.20.0/24` | `192.168.20.1` |
| Informatique | 30 | `192.168.30.0/24` | `192.168.30.1` |
| Agence | aucun | `192.168.40.0/24` | `192.168.40.1` |
| `SW-L3` ↔ `R-SIEGE` | aucun | `10.0.1.0/30` | |
| `R-SIEGE` ↔ `R-AGENCE` | aucun | `10.0.0.0/30` | |

## Étapes
* Étape 1 : je conçois la topologie et le plan d'adressage ([détails](docs/01-conception.md))
* Étape 2 : je pose les équipements et je les câble ([détails](docs/02-topologie.md))
* Étape 3 : je crée les VLAN et j'affecte les ports du switch ([détails](docs/03-vlans.md))
* Étape 4 : je fais communiquer les VLAN entre eux ([détails](docs/04-routage-inter-vlan.md))
* Étape 5 : je relie le siège et l'agence et je configure le routage ([détails](docs/05-routeurs-routage.md))
* Étape 6 : je configure le DHCP ([détails](docs/06-dhcp.md))
* Étape 7 : je teste la connectivité entre les deux sites ([détails](docs/07-tests-connectivite.md))

## Résultat
- `PC-DIR1` joint `PC-AGENCE` : 4 réponses sur 4 au second essai.
- `tracert` depuis `PC-DIR1` montre le chemin `SW-L3` → `R-SIEGE` → `R-AGENCE` → `PC-AGENCE`.
- Les 5 postes reçoivent leur adresse en DHCP.

## Difficultés rencontrées
| Étape | Difficulté | Détail |
|---|---|---|
| 3 | Fautes de frappe et oubli de `switchport mode access` | [docs/03-vlans.md](docs/03-vlans.md) |
| 4 | `interface vlan 3` au lieu de `interface vlan 30` | [docs/04-routage-inter-vlan.md](docs/04-routage-inter-vlan.md) |
| 5 | Commandes tapées dans le mauvais routeur, espaces remplacés par des points, RIP activé par erreur | [docs/05-routeurs-routage.md](docs/05-routeurs-routage.md) |
| 7 | Test « même VLAN » qui pingue le poste lui-même | [docs/07-tests-connectivite.md](docs/07-tests-connectivite.md) |

## Compétences mises en pratique
- Créer des VLAN et affecter des ports d'accès
- Configurer le routage entre VLAN avec des interfaces virtuelles (SVI)
- Écrire des routes statiques et une route par défaut
- Configurer un service DHCP avec exclusions d'adresses
- Diagnostiquer avec `ping`, `tracert` et `show ip route`

## Contenu du dépôt
- `docs/` : une page par étape, avec les captures de preuve
- `screenshots/` : captures utilisées dans les pages
- `packet-tracer/` : fichier du laboratoire (`.pkt`)
