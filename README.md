# LAB 2 : Rooting Android

## 📌 Objectif du lab

Comprendre ce qu'est le rooting sur Android, comment le réaliser sur un environnement de test (émulateur), identifier les impacts sur la sécurité, et documenter les risques et mesures de protection associés.

---

## 🎯 Ce que nous avons appris

| Concept | Définition |
|---------|-------------|
| **Root** | Privilèges super-utilisateur sur Android (équivalent de l'administrateur sur Windows) |
| **Verified Boot** | Mécanisme qui vérifie l'intégrité du système au démarrage |
| **AVB** | Android Verified Boot (version 2.0) avec partition `vbmeta` et protection anti-rollback |
| **Chaîne de confiance** | Série de vérifications où chaque composant vérifie l'authenticité du suivant |
| **adb root** | Commande qui active le serveur ADB avec les privilèges root |

---

## 🛠️ Environnement de test

| Élément | Valeur |
|---------|--------|
| **Support** | AVD (émulateur Genymotion) |
| **Modèle** | Samsung Galaxy Note 10plus |
| **Android** | 9.0 (Pie) - API 28 |
| **Application testée** | OWASP UnCrackable Level 1 |
| **Package** | `owasp.mstg.uncrackable1` |

---

## 🔧 Commandes essentielles

```bash
# Vérifier la connexion
adb devices

# Activer le mode root
adb root

# Vérifier les privilèges (uid=0 = root)
adb shell id

# Remonter la partition système en lecture/écriture
adb remount

# Installer une application
adb install UnCrackable-Level1.apk

# Lancer une application
adb shell am start -n owasp.mstg.uncrackable1/sg.vantagepoint.uncrackable1.MainActivity

# Voir les logs
adb logcat -d | grep -i "uncrackable" | tail -30

# Éteindre l'émulateur
adb shell reboot -p
```

## 🔍 Définition du rooting (4 phrases)

Le rooting est le processus qui permet d'obtenir les privilèges super-utilisateur (root) sur un système Android. Cela modifie les protections natives et brise la chaîne de confiance établie par Verified Boot. En laboratoire, le rooting est utile pour observer certains comportements d'application face à un attaquant privilégié. Cependant, cette pratique est risquée et nécessite un isolement strict, une traçabilité complète et une remise à zéro systématique après chaque session.

---


## 🔗 Verified Boot et Chaîne de confiance


### Chaîne de confiance

Chaque composant (ROM, Bootloader, Kernel, Système) vérifie l'authenticité du suivant avant de lui passer la main. Si un maillon est modifié, la vérification échoue.

### AVB – Android Verified Boot

AVB (version 2.0) utilise la partition `vbmeta` pour centraliser les hachés des partitions critiques et ajoute une protection anti-rollback empêchant l'installation de versions vulnérables.

---

## ❗ Pourquoi l'intégrité au démarrage est critique ?

Si le démarrage est compromis, toutes les protections ultérieures (sandbox, permissions, chiffrement) peuvent être contournées. Un attaquant avec un bootloader modifié peut désactiver les sécurités dès le lancement du système.


## ⚠️ Matrice des 8 risques du rooting

| # | Risque | Impact |
|---|--------|--------|
| 1 | Intégrité non garantie | Conclusions biaisées sur la sécurité réelle |
| 2 | Surface d'attaque accrue | Malware avec contrôle total |
| 3 | Exposition des données sensibles | Accès global aux données des apps |
| 4 | Instabilité système | Crashs, boot loops |
| 5 | Mélange comptes perso/test | Fuite de données personnelles |
| 6 | Mauvais nettoyage | Contamination des tests suivants |
| 7 | Réseau non isolé | Risque pour d'autres machines |
| 8 | Traçabilité insuffisante | Tests non reproductibles |


## 🛡️ Mesures défensives appliquées

| # | Mesure | Objectif |
|---|--------|----------|
| 1 | Réseau isolé (Host-Only) | Communications contrôlées |
| 2 | Données fictives | Zéro fuite réelle |
| 3 | Appareil dédié | Isolation totale |
| 4 | Wipe systématique | Aucun résidu |
| 5 | Journal détaillé | Reproductibilité |
| 6 | Aucun compte personnel | Protection vie privée |
| 7 | APK contrôlés | Éviter malwares |
| 8 | Captures horodatées | Traçabilité |


## 📚 Références OWASP (MASVS / MASTG)

### Exigences MASVS

| Exigence | Description | Lien avec le rooting |
|----------|-------------|----------------------|
| MASVS-STORAGE-1 | Stockage sécurisé | `/data/data/` accessible en root ⇒ chiffrement nécessaire |
| MASVS-CODE-1 | Détection du root | L'app doit détecter/refuser l'exécution |

### Idées de tests MASTG

| Test | Méthode | Outils |
|------|---------|--------|
| Lecture des données app | Explorer `/data/data/<package>` | `adb shell`, `su`, `cat` |
| Détection du root | Comparaison root / non-root | `adb shell am start` |


## 📸 Preuves (screenshots)

### Rooting

<img width="1304" height="517" alt="Rooting1" src="https://github.com/user-attachments/assets/b01c8b5a-252f-48e4-977a-99e3938d9b03" />
<img width="609" height="215" alt="Rooting2" src="https://github.com/user-attachments/assets/efe18c96-f7a6-4290-8b7a-4e7a95542cdb" />

### Verified Boot
<img width="552" height="436" alt="Verified_Boot" src="https://github.com/user-attachments/assets/6c3441f7-797b-4edc-968f-753574b6ea1a" />

### APK
<img width="1202" height="415" alt="Apk_Inst1" src="https://github.com/user-attachments/assets/8826942b-e358-45d7-b22e-e190fea287ac" />
<img width="1203" height="469" alt="Apk_Inst2" src="https://github.com/user-attachments/assets/d0f29090-be83-44e5-ac1c-29ae36f3c333" />
<img width="1384" height="835" alt="Apk_test" src="https://github.com/user-attachments/assets/17781c39-1f4c-4500-879c-c933e683f652" />
<img width="1600" height="653" alt="Apk_test2" src="https://github.com/user-attachments/assets/64deb53b-c03b-46e1-8ad9-392105e4975f" />

### Idées de tests MASTG
<img width="708" height="412" alt="test1" src="https://github.com/user-attachments/assets/bf6a3117-909b-4b1e-bd3e-2a0087dd9538" />
<img width="1586" height="625" alt="test2" src="https://github.com/user-attachments/assets/e41eeb1c-fb4b-4578-817e-158045074c72" />

### Remise à zéro AVD
<img width="447" height="222" alt="etteint" src="https://github.com/user-attachments/assets/5c834834-b77e-4517-bb73-ac2162778da9" />



## ✅ Checklist

### Début de lab

| Vérification | Statut |
|--------------|--------|
| Périmètre défini | ✅ |
| AVD neuf | ✅ |
| App installée | ✅ |
| Scénarios définis | ✅ |
| Versions notées | ✅ |

### Fin de lab

| Vérification | Statut |
|--------------|--------|
| Données supprimées | ✅ |
| Wipe AVD effectué | ✅ |
| Capture preuve reset | ✅ |
| Aucun compte personnel | ✅ |


---


## 📄 Fiche environnement

| Champ | Valeur |
|-------|--------|
| **Date** | 2026-04-17 |
| **Auteur** | El Hachimi Abdelhamid |
| **Objectif** | Comprendre le rooting, ses impacts et les mécanismes de sécurité Android |
| **Support** | AVD (émulateur Genymotion) |
| **Modèle** | Samsung Galaxy Note 10plus |
| **Android** | 9.0 (Pie) - API 28 |
| **App testée** | OWASP UnCrackable Level 1 |
| **Package** | `owasp.mstg.uncrackable1` |
| **Version** | 1.0 |
| **Root activé** | `adb root` → `adbd is already running as root` |
| **UID root** | `adb shell id` → `uid=0(root)` |
| **Comportement app** | Détection du root → message → fermeture |

> La fiche environnement complète est disponible dans [`fiche_environnement_lab2.md`](fiche_environnement_lab2.md)




## 👤 Auteur

**El Hachimi Abdelhamid**  
Date : 2026-04-17  
Cours : Sécurité des applications mobiles

---


