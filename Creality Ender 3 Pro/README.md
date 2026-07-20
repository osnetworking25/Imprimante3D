# Creality Ender 3 Pro (carte mère 4.2.7) — Firmware avec BLTouch

## Contexte

Ce projet consiste à préparer un firmware Marlin avec BLTouch pour une Ender 3 Pro équipée d'une carte mère **4.2.7** (32 bits, silencieuse, drivers TMC2208/2225, écran CR10_STOCKDISPLAY).

## Ce qu'on a appris sur cette carte

- Creality ne publie **aucun code source** pour ses cartes 32 bits (4.2.2 / 4.2.7) — seuls des fichiers `.bin` précompilés sont disponibles. Le fichier "Source Code" fourni sur leur site ne concerne que l'ancienne carte 8 bits (v1.1.6.1, 2019). C'est un vrai problème de conformité à la licence GPL, déjà signalé par des développeurs Marlin eux-mêmes.
- Il existe deux variantes de puce sur cette carte : **RE (512K de flash)** et **RC (256K)**. On les distingue uniquement par le texte gravé sur la puce STM32 elle-même : `RET6` = RE, `RCT6` = RC. Il faut ouvrir l'imprimante et regarder la puce avant de compiler, sinon le firmware ne fonctionnera pas.
- Dans `platformio.ini`, la valeur par défaut `default_envs = mega2560` correspond aux anciennes cartes 8 bits (AVR) — elle doit être changée en `STM32F103RE_creality` ou `STM32F103RC_creality` selon la puce, sinon la compilation échoue avec une erreur d'environnement incompatible.

## Reprise du firmware Marlin 2.1.2.8 (bugfix)

Firmware construit à partir des sources Marlin officielles + configuration Creality V427, avec BLTouch activé :

**Nivellement et sécurité**
- `BLTOUCH`, `AUTO_BED_LEVELING_BILINEAR`, `Z_SAFE_HOMING`
- `PROBE_OFFSET_WIZARD` (assistant de calibration Z à l'écran)

**Confort / menus**
- `PRINTCOUNTER`, `INDIVIDUAL_AXIS_HOMING_MENU`
- `LCD_INFO_MENU` (écran "à propos")
- `POWER_LOSS_RECOVERY`, `SOUND_MENU_ITEM`, `SDCARD_SORT_ALPHA`
- `BABYSTEP_ALWAYS_AVAILABLE` + `BABYSTEP_ZPROBE_OFFSET` (le babystep modifie et sauvegarde directement l'offset Z de la sonde)
- `LIN_ADVANCE`

## Étapes avant de flasher pour de vrai

1. Identifier la puce (RE ou RC) et ajuster `platformio.ini` en conséquence.
2. Monter le BLTouch, mesurer les offsets X/Y au pied à coulisse (buse ↔ centre de la sonde).
3. Vérifier l'ordre des fils du connecteur BLTouch (peut varier selon le fabricant).
4. Flasher via carte SD (fichier `.bin` à la racine, FAT32).
5. Régler l'offset Z par le test du papier.

## Astuce VS Code : un profil par imprimante

Pour éviter de mélanger les configurations entre plusieurs imprimantes dans VS Code, on peut créer un **profil dédié** (Gérer ⚙ → Profils → Nouveau profil), le nommer, copier le contenu du profil "Par défaut" (pour garder les extensions comme PlatformIO), puis l'associer au dossier du projet via "Ajouter un dossier". VS Code bascule alors automatiquement sur le bon profil à l'ouverture du dossier.
