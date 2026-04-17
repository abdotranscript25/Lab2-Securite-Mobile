# FICHE ENVIRONNEMENT - LAB 2 (Rooting Android)

## 1. Informations générales
| Champ | Valeur |
|-------|--------|
| **Date** | 2026-04-17 |
| **Auteur** | El Hachimi Abdelhamid |
| **Objectif** | Comprendre le rooting, ses impacts et les mécanismes de sécurité Android |

## 2. Support de test
| Champ | Valeur |
|-------|--------|
| **Type** | AVD (émulateur) |
| **Nom** | Genymotion - Samsung Galaxy Note 10plus |
| **Version Android** | 9.0 (Pie) |
| **API** | 28 |
| **Architecture** | x86 |

## 3. Application testée
| Champ | Valeur |
|-------|--------|
| **Nom** | OWASP UnCrackable Level 1 |
| **Package** | owasp.mstg.uncrackable1 |
| **Version** | 1.0 |
| **Source** | OWASP MSTG Crackmes |

## 4. Scénarios de test
| # | Scénario | Action | Résultat observé | Statut |
|---|----------|--------|------------------|--------|
| 1 | Lancement normal | Lancement de l'app sur émulateur rooté | Message "Root detected!" puis fermeture | ✅ Testé |

| 2 | Analyse des logs | db logcat -d \| grep -i "root" | Traces de "Root detected!" et "System.exit" | ✅ Testé |

| 3 | Contournement (Frida) | (Futur lab) | À venir | ⏳ Lab suivants |

## 5. Observations factuelles
| Observation | Détail |
|-------------|--------|
| Root activé | db root → dbd is already running as root |
| UID root | db shell id → uid=0(root) |
| Partition /system | db remount → 
emount succeeded |
| Comportement app | Détection du root → affichage message → fermeture |
| Logs clés | System.exit called, status: 0 puis Process has died |

## 6. Commandes exécutées
db devices
db root
db shell id
db remount
db install UnCrackable-Level1.apk
db shell am start -n owasp.mstg.uncrackable1/sg.vantagepoint.uncrackable1.MainActivity
db logcat -d | grep -i "uncrackable" | tail -30
db logcat -d | grep -i "root" | tail -20

## 7. Limites de l'environnement
| Limite | Explication |
|--------|-------------|
| AVD non représentatif | L'émulateur n'a pas de véritable chaîne de confiance matérielle |
| Pas de test sur vrai appareil | Les conclusions peuvent différer sur matériel réel |
| Root "facile" | Sur AVD, db root fonctionne directement |


## 8. Nettoyage effectué

| Action | Effectué ? | Preuve |
|--------|------------|--------|
| Émulateur éteint (db shell reboot -p) | ✅ | screenshots/08_avd_shutdown.png |
| Wipe data dans Genymotion | ✅ | screenshots/09_avd_wipe_data.png |
| Redémarrage état neuf | ✅ | screenshots/10_avd_clean_state.png |
| Désinstallation de l'APK | ✅ | db uninstall owasp.mstg.uncrackable1 |

## 9. Vérification des livrables - Screenshots

Le dossier screenshots/ contient toutes les captures d'écran du laboratoire :

## 10. Signature et validation

**Je soussigné(e) El Hachimi Abdelhamid certifie avoir réalisé cette analyse dans le respect du périmètre autorisé et des règles éthiques définies.**

**Date** : 2026-04-17
**Signature** : El Hachimi Abdelhamid
