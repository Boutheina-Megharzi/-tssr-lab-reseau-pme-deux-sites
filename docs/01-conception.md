# Étape 1 : conception du réseau

## Objectif
Je conçois le réseau d'une PME fictive répartie sur deux sites, avant de le construire dans Packet Tracer.

## Contexte (scénario fictif)
Une PME fictive a son siège à Lyon et une agence à Grenoble. Le siège compte trois services : Direction, Comptabilité et Informatique. L'agence compte un poste. Les postes de l'agence doivent travailler avec ceux du siège.

## Cahier des charges
- Séparer les trois services du siège dans des VLAN distincts.
- Permettre aux services de communiquer entre eux.
- Relier le siège et l'agence.
- Distribuer les adresses IP automatiquement avec un service DHCP.
- Tester la connectivité entre tous les postes.

## Notions utilisées
- **VLAN** : réseau virtuel dans un switch. Il sépare les services sans acheter un switch par service.
- **Sous-réseau** : plage d'adresses, par exemple `192.168.10.0/24`.
- **Passerelle** : adresse du routeur par laquelle un poste sort de son réseau.
- **Switch de niveau 3** : switch qui route aussi entre les VLAN.
- **Routage statique** : routes écrites à la main.

## Topologie prévue
```
                 SIÈGE (Lyon)                                    AGENCE (Grenoble)
 PC-DIR1 ──┐
 PC-DIR2 ──┤
 PC-CPT  ──┼── SW-L3 ───── R-SIEGE ═══════════ R-AGENCE ───── SW2 ──── PC-AGENCE
 PC-INF  ──┘   VLAN 10/20/30      liaison 10.0.0.0/30
```

## Plan d'adressage
| Réseau | VLAN | Adresse réseau | Passerelle |
|---|---|---|---|
| Direction | 10 | `192.168.10.0/24` | `192.168.10.1` |
| Comptabilité | 20 | `192.168.20.0/24` | `192.168.20.1` |
| Informatique | 30 | `192.168.30.0/24` | `192.168.30.1` |
| Agence | aucun | `192.168.40.0/24` | `192.168.40.1` |
| Liaison `SW-L3` ↔ `R-SIEGE` | aucun | `10.0.1.0/30` | `R-SIEGE` : `10.0.1.1`, `SW-L3` : `10.0.1.2` |
| Liaison `R-SIEGE` ↔ `R-AGENCE` | aucun | `10.0.0.0/30` | `R-SIEGE` : `10.0.0.1`, `R-AGENCE` : `10.0.0.2` |

## Choix de conception
- Je choisis des adresses privées en `192.168.x.0/24`, un réseau par service, faciles à lire.
- Je relie les deux routeurs avec un `/30` : il n'offre que deux adresses utilisables, juste ce qu'il faut.
- Je route entre les VLAN avec le switch de niveau 3 `SW-L3`.
- Je n'écris aucun accent dans les noms d'équipements.

## Vérifications
- Chaque sous-réseau est différent des autres.
- Chaque passerelle appartient bien à son réseau.
- Les deux liaisons entre équipements sont en `/30`.

## Prochaine étape
Je pose les équipements dans Packet Tracer et je les câble.
