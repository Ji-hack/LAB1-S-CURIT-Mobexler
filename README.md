# LAB1-SÉCURITÉ — Mobexler

## Présentation de l'environnement

Mobexler est une machine virtuelle dédiée aux tests de sécurité sur applications mobiles Android et iOS. Construite sur une base Linux allégée, elle centralise l'ensemble de la chaîne d'outils nécessaire à un audit mobile dans un seul environnement opérationnel, éliminant toute configuration préalable.

Elle fonctionne sous VirtualBox ou VMware et s'exécute indifféremment depuis un hôte Windows, macOS ou Linux.

---

## Problématique et apport

Construire un lab de pentest mobile manuellement implique une série de contraintes : installation individuelle d'ADB, Frida, Burp Suite, apktool ou encore jadx, gestion des incompatibilités entre versions, configuration des certificats proxy sur l'émulateur, et patching manuel des APKs.

Mobexler supprime cette friction. L'ensemble des outils arrive pré-installé et pré-configuré — on démarre la VM, on teste.

---

## Outillage embarqué

| Domaine | Outils |
|---|---|
| Analyse statique | jadx, apktool, dex2jar, androguard |
| Analyse dynamique | Frida, objection, Xposed |
| Proxy / Réseau | Burp Suite, mitmproxy, Wireshark |
| ADB & SDK | adb, Android SDK tools |
| Reverse engineering | Ghidra, strings, binwalk |
| Exploitation | Metasploit, drozer |
| Utilitaires | Python3, Node.js, Git, VS Code |

---

## Schéma d'architecture

```
┌─────────────────────────────────┐
│        PC Hôte (Windows)        │
│                                 │
│  ┌──────────────────────────┐   │
│  │   Android Studio AVD     │   │
│  │   (émulateur Android)    │   │
│  └────────────┬─────────────┘   │
│               │ ADB (TCP)       │
│  ┌────────────▼─────────────┐   │
│  │     VM Mobexler          │   │
│  │  (outils de pentest)     │   │
│  │  IP : 10.0.2.15          │   │
│  │  Gateway hôte : 10.0.2.2 │   │
│  └──────────────────────────┘   │
└─────────────────────────────────┘
```

La VM Mobexler dialogue avec l'émulateur via ADB over TCP pour analyser, intercepter et manipuler l'application cible.

---

## Scénarios d'usage typiques

- **DIVA** (Damn Insecure and Vulnerable App) — terrain d'entraînement aux vulnérabilités Android classiques
- **Interception HTTPS** — capture du trafic applicatif via Burp Suite avec certificat injecté dans l'émulateur
- **Hooking dynamique avec Frida** — contournement de la détection root ou du SSL pinning à la volée
- **Décompilation APK avec jadx** — lecture du bytecode Java/Kotlin même après obfuscation
- **Audit des stockages locaux** — détection de données sensibles exposées dans SharedPreferences, SQLite ou fichiers bruts

---

## Connexion ADB entre Mobexler et l'émulateur

L'émulateur s'exécutant côté hôte Windows, on passe par l'IP de la gateway VirtualBox.

Depuis le terminal Mobexler :
```bash
adb connect 10.0.2.2:5555
adb devices
```

Depuis l'invite de commandes Windows :
```cmd
adb forward tcp:5555 tcp:5554
```

---

## Captures du lab

`devices` · `demarrage` · `accueil` · `snapshot` · `ip` · `installation de mobexler` · `import-mobexler` · `hash`



<img width="895" height="673" alt="image" src="https://github.com/user-attachments/assets/0fc45b71-2faa-4622-8fe4-72bf49c455ce" />

<img width="308" height="341" alt="image" src="https://github.com/user-attachments/assets/2027965b-e948-4c9a-bf0d-ebb1e19b7453" />
![Uploading image.png…]()



