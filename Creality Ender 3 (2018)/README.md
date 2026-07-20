# Creality Ender 3 (2018) — passage à Klipper (BigTreeTech Manta E3EZ+ / CB1)
*Creality Ender 3 (2018) — Klipper upgrade (BigTreeTech Manta E3EZ+ / CB1)*

> 🇫🇷 Mon Ender 3 d'origine (2018), mise à niveau avec une carte BigTreeTech Manta E3EZ+ et un module CB1 pour passer sous Klipper. Documentation en cours de constitution.
> 🇬🇧 My original Ender 3 (2018), upgraded with a BigTreeTech Manta E3EZ+ board and a CB1 module to run Klipper. Documentation in progress.

---

## Contexte

Mon Ender 3 d'origine (2018), modèle de base (pas la version "Pro"), dont la carte mère 8 bits d'origine est remplacée par un kit BigTreeTech orienté Klipper.

## Matériel installé

- **Carte mère : BigTreeTech Manta E3EZ+** — carte 32 bits pensée pour Klipper, version "EZ" (câblage simplifié) et "+" (support CB1 intégré).
- **Module CB1** — SoM (System on Module) BigTreeTech compatible Raspberry Pi CM4, qui fait tourner l'hôte Klipper directement sur la carte (pas besoin de Raspberry Pi séparé).
- **Extrudeur : H2V2S**
- **Sonde de nivellement : BigTreeTech MicroProbe V2** (sonde à courant de Foucault, alternative au BLTouch)
- **Écran : TFT35 SPI V2.1**
- **Universal Turbo Kit** (kit de refroidissement/ventilation buse)
- **Drivers moteurs : TMC2209** — ⚠️ à vérifier attentivement (mode UART/standalone, réglage du courant, sensorless homing) avant la première mise en route.

## Différence importante avec le projet Ender 3 Pro

Contrairement à l'Ender 3 Pro (firmware **Marlin** compilé via PlatformIO), cette machine tourne sous **Klipper** : la configuration se fait via un fichier `printer.cfg` (et non un `Configuration.h`), et le nivellement/la sonde sont gérés différemment (MicroProbe au lieu du BLTouch).

## État actuel

Matériel installé, configuration Klipper à documenter (câblage, `printer.cfg`, calibration de la sonde MicroProbe V2, mise en service de l'écran TFT35 en mode tactile).

## À compléter plus tard

- Câblage détaillé du Manta E3EZ+ (pinout extrudeur H2V2S, MicroProbe V2, TFT35).
- Fichier `printer.cfg` Klipper complet et commenté.
- Étapes de calibration de la sonde MicroProbe V2 (offsets, mesh bed leveling).
- Configuration de l'écran TFT35 SPI V2.1 (mode KlipperScreen ou mode tactile natif).
- Retour d'expérience sur le Universal Turbo Kit (montage, refroidissement obtenu).
- Détails sur la configuration des drivers TMC2209 (à préciser).

## Licence / License

MIT — voir / see [LICENSE](../LICENSE).

---

# English version

## Context

My original Ender 3 (2018), base model (not the "Pro" version), whose original 8-bit motherboard is being replaced with a BigTreeTech kit built for Klipper.

## Installed hardware

- **Motherboard: BigTreeTech Manta E3EZ+** — 32-bit board designed for Klipper, "EZ" variant (simplified wiring) and "+" (built-in CB1 support).
- **CB1 module** — BigTreeTech System-on-Module, Raspberry Pi CM4-compatible, running the Klipper host directly on the board (no separate Raspberry Pi needed).
- **Extruder: H2V2S**
- **Leveling probe: BigTreeTech MicroProbe V2** (eddy-current probe, an alternative to BLTouch)
- **Screen: TFT35 SPI V2.1**
- **Universal Turbo Kit** (part-cooling fan duct kit)
- **Stepper drivers: TMC2209** — ⚠️ double-check carefully (UART/standalone mode, current setting, sensorless homing) before first power-up.

## Key difference from the Ender 3 Pro project

Unlike the Ender 3 Pro (**Marlin** firmware compiled via PlatformIO), this machine runs **Klipper**: configuration is done through a `printer.cfg` file (not a `Configuration.h`), and leveling/probing are handled differently (MicroProbe instead of BLTouch).

## Current status

Hardware installed; Klipper configuration still to be documented (wiring, `printer.cfg`, MicroProbe V2 calibration, bringing up the TFT35 screen in touch mode).

## To complete later

- Detailed Manta E3EZ+ wiring (H2V2S extruder pinout, MicroProbe V2, TFT35).
- Full, commented Klipper `printer.cfg` file.
- MicroProbe V2 calibration steps (offsets, mesh bed leveling).
- TFT35 SPI V2.1 screen setup (KlipperScreen mode or native touch mode).
- Field notes on the Universal Turbo Kit (assembly, cooling results).
- TMC2209 driver configuration details (to be specified).

## License

MIT — see LICENSE file in the parent folder.
