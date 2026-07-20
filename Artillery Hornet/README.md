# Artillery Hornet — Firmware avec BLTouch
*Artillery Hornet — Firmware with BLTouch*

> 🇫🇷 Retour d'expérience sur l'ajout d'un BLTouch à mon Artillery Hornet : réglages Marlin, problèmes rencontrés (sonde bloquée, nivellement non appliqué) et leurs solutions.
> 🇬🇧 Field notes on adding a BLTouch to my Artillery Hornet: Marlin settings, problems encountered (stuck probe, leveling not applied) and their fixes.

---

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

## Licence / License

MIT — voir / see [LICENSE](../LICENSE).

---

# English version

## Context

My own Artillery Hornet (Ruby motherboard), on which I added a BLTouch and compiled a custom Marlin firmware.

## Settings added (Phase 1: leveling and convenience)

The same package of options was later reused as a base for the Ender 3 Pro project (see the neighboring folder):

BLTOUCH, AUTO_BED_LEVELING_BILINEAR, Z_SAFE_HOMING, PROBE_OFFSET_WIZARD, LCD_INFO_MENU, POWER_LOSS_RECOVERY, SOUND_MENU_ITEM, SDCARD_SORT_ALPHA, BABYSTEP_ALWAYS_AVAILABLE plus BABYSTEP_ZPROBE_OFFSET, and LIN_ADVANCE.

## Problems encountered and solutions (field notes)

This section is the most useful part if someone else runs into the same symptoms:

1. The Z probe stayed permanently stuck on "TRIGGERED". The Ruby board uses the same pin for the Z endstop and the BLTouch probe by default (Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN), which caused issues. Fix: use a dedicated pin for the probe (Z_MIN_PROBE_PIN PC2 on this board) instead of sharing the endstop pin.

2. The printer had to be plugged into AC power for the probe to work properly. Surprising discovery: on weak/battery power, the BLTouch did not behave normally. Worth checking if behavior seems erratic.

3. Bed leveling was not applied to prints. The slicer's start G-code did not include M420 S1 after G28. Without this command, Marlin does build a bed mesh but does not apply it to the print. A classic and easy-to-forget pitfall.

4. ArtillerySlicer refused to save the modified start G-code. ArtillerySlicer's system profiles are locked for writing. Fix: use "Save as" to create a custom profile, then select it.

## Calibration values (last recorded)

Probe X offset: -55.3. Probe Y offset: 0. Probe Z offset: -1.4.

These values are specific to my probe and my setup, so they should not be reused as-is on another printer, but they give an order of magnitude.

## License

MIT — see LICENSE file in the parent folder.
