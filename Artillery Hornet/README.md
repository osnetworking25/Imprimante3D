# Artillery Hornet — Firmware avec BLTouch

## Contexte

Ma propre Artillery Hornet (carte mère Ruby), sur laquelle j'ai ajouté un BLTouch et compilé un firmware Marlin personnalisé.

## Réglages ajoutés (Phase 1 — nivellement et confort)

Le même paquet d'options a servi de base pour le projet Ender 3 Pro (voir le dossier voisin) :

- `BLTOUCH`, `AUTO_BED_LEVELING_BILINEAR`, `Z_SAFE_HOMING`
- `PROBE_OFFSET_WIZARD`, `LCD_INFO_MENU`
- `POWER_LOSS_RECOVERY`, `SOUND_MENU_ITEM`, `SDCARD_SORT_ALPHA`
- `BABYSTEP_ALWAYS_AVAILABLE` + `BABYSTEP_ZPROBE_OFFSET`
- `LIN_ADVANCE`

## Problèmes rencontrés et solutions (retour d'expérience)

Cette partie est la plus utile si quelqu'un d'autre tombe sur les mêmes symptômes :

**1. La sonde Z restait bloquée en "TRIGGERED" en permanence**
La carte Ruby utilise par défaut la même broche pour l'endstop Z et la sonde BLTouch (`Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN`). Ça posait problème. Solution : utiliser une broche dédiée pour la sonde (`Z_MIN_PROBE_PIN PC2` sur cette carte) au lieu de partager la broche d'endstop.

**2. L'imprimante devait être branchée sur secteur (AC) pour que la sonde fonctionne**
Découverte surprenante : sur batterie/alimentation faible, le BLTouch ne se comportait pas normalement. À vérifier si le comportement semble erratique.

**3. Le nivellement ne s'appliquait pas à l'impression**
Le G-code de démarrage du slicer n'incluait pas `M420 S1` après le `G28` — sans cette commande, Marlin fait bien un maillage du plateau (bed mesh) mais ne l'applique pas à l'impression. Piège classique et facile à oublier.

**4. ArtillerySlicer refusait de sauvegarder le G-code de démarrage modifié**
Les profils système d'ArtillerySlicer sont verrouillés en écriture. Solution : utiliser "Enregistrer sous" pour créer un profil personnalisé, puis le sélectionner.

## Valeurs de calibration (dernier relevé)

- Offset sonde X : **-55.3**
- Offset sonde Y : **0**
- Offset sonde Z : **-1.4**

Ces valeurs sont propres à ma sonde et mon montage — à ne pas réutiliser telles quelles sur une autre imprimante, mais elles donnent un ordre de grandeur.
