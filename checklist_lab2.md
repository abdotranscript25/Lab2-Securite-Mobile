# CHECKLIST FINALE - LAB 2 (Rooting Android)

**Auteur** : El Hachimi Abdelhamid
**Date** : 2026-04-17

---

## 📋 Début de séance

| # | Vérification | Statut | Commentaire |
|---|--------------|--------|-------------|
| 1 | Périmètre écrit et documenté | ✅ | Fiche environnement section 1 |
| 2 | AVD neuf (émulateur propre) | ✅ | Genymotion - Android 9.0 |
| 3 | App test installée | ✅ | OWASP UnCrackable Level 1 |
| 4 | 3 scénarios de test notés | ✅ | Lancement, Logs, Contournement |
| 5 | Version Android documentée | ✅ | API 28 (Android 9.0) |
| 6 | Version app documentée | ✅ | UnCrackable Level 1 v1.0 |

---

## 🔧 Pendant le lab

| # | Vérification | Statut | Commentaire |
|---|--------------|--------|-------------|
| 7 | Root activé (db root) | ✅ | dbd is already running as root |
| 8 | Vérification UID root (db shell id) | ✅ | uid=0(root) |
| 9 | Remontage partition (db remount) | ✅ | 
emount succeeded |
| 10 | Installation de l'APK | ✅ | Success |
| 11 | Lancement de l'application | ✅ | Message "Root detected!" |
| 12 | Capture des logs | ✅ | System.exit called, status: 0 |
| 13 | Accès au dossier /data/data/ | ✅ | Avec su |

---

## 🧹 Fin de séance (Nettoyage)

| # | Vérification | Statut | Preuve |
|---|--------------|--------|--------|
| 14 | Émulateur éteint | ✅ | db shell reboot -p |
| 15 | Wipe data effectué | ✅ | Genymotion → Wipe data |
| 16 | Redémarrage état neuf | ✅ | Capture écran d'accueil |
| 17 | Aucun compte personnel utilisé | ✅ | Pas de compte Google connecté |

---



---

## 📊 Résumé des livrables

| Livrable | Emplacement | Statut |
|----------|-------------|--------|
| Fiche environnement | fiche_environnement_lab2.md | ✅ |
| Définition rooting (4 phrases) | Section dans rapport | ✅ |
| Schéma Verified Boot/AVB | Section dans rapport | ✅ |
| 8 risques + 8 mesures | Section dans rapport | ✅ |
| MASVS (2 exigences) | Section dans rapport | ✅ |
| MASTG (2 tests) | Section dans rapport | ✅ |
| Screenshots | screenshots/ (8 fichiers) | ✅ |

---

## ✅ Validation finale

**Je soussigné(e) El Hachimi Abdelhamid certifie avoir réalisé cette analyse dans le respect du périmètre autorisé et des règles éthiques définies.**

- **Date** : 2026-04-17
- **Signature** : El Hachimi Abdelhamid
- **Environnement** : Genymotion (Android 9.0, API 28)
- **App testée** : OWASP UnCrackable Level 1

---

## 📝 Méthodologie PDCA

| Phase | Action | Statut |
|-------|--------|--------|
| **Plan** | Périmètre écrit, scénarios définis | ✅ |
| **Do** | Exécution des tests (root, installation, lancement) | ✅ |
| **Check** | Vérification des logs, captures d'écran | ✅ |
| **Act** | Nettoyage, wipe data, documentation | ✅ |

---

*Document généré le 2026-04-17 dans le cadre du LAB 2 - Rooting Android*
