# Blackwall Lab Backup

**Sauvegardes personnelles chiffrées, avec stockage distant sur Google Drive.**

Blackwall Lab Backup est une application OAuth personnelle utilisée pour autoriser **Rclone** à transférer des sauvegardes **chiffrées localement par Restic** vers Google Drive.

Ce dépôt héberge uniquement le **site de présentation public** de l'application et sa politique de confidentialité, via GitHub Pages. Il ne contient ni coffre-fort, ni sauvegarde, ni identifiant de connexion.

🌐 **Site :** https://zelest.github.io/

🔐 **Confidentialité :** https://zelest.github.io/privacy.html

## Comment ça fonctionne ?

Le processus de sauvegarde prévu se déroule en trois étapes.

### 1. Préparer les données

Les données importantes du homelab — en priorité celles de **Vaultwarden** — sont regroupées pour la sauvegarde.

Pour Vaultwarden, cela implique notamment une copie cohérente de la base de données, des pièces jointes et des éléments de configuration nécessaires à une restauration.

Une **sauvegarde locale du conteneur Proxmox** est également conservée pour faciliter une restauration rapide.

### 2. Chiffrer avec Restic

**Restic** crée des sauvegardes chiffrées avant leur transfert.

Il prend en charge les instantanés, la déduplication et la conservation de plusieurs versions pour pouvoir revenir à un état antérieur.

La clé de déchiffrement doit être conservée **séparément** du serveur et du dépôt de sauvegarde. Perdre cette clé signifie ne plus pouvoir restaurer les données.

### 3. Transférer avec Rclone

**Rclone** sert de liaison avec Google Drive.

L'application OAuth Blackwall Lab Backup lui accorde l'autorisation `drive.file`, limitée aux fichiers Google Drive créés ou ouverts par l'application.

Google Drive sert de stockage distant : **l'objectif est de n'y envoyer que le dépôt chiffré Restic**, jamais une exportation en clair du coffre-fort.

**Chaîne de sauvegarde :**

Vaultwarden → Copie cohérente → Restic (chiffrement local) → Rclone → Google Drive

## Sécurité et confidentialité

- **Usage personnel uniquement :** aucune inscription publique ni service de sauvegarde proposé à des tiers.
- **Chiffrement avant transfert :** les sauvegardes sont protégées localement par Restic avant leur envoi.
- **Accès Google limité :** l'autorisation OAuth `drive.file` n'accorde pas un accès général à l'ensemble de Google Drive.
- **Secrets hors du dépôt :** aucun mot de passe, jeton OAuth, Client Secret, fichier de configuration Rclone ou clé Restic n'est publié ici.
- **Restauration indispensable :** une sauvegarde n'est considérée comme fiable qu'après un test de restauration.

La [politique de confidentialité](https://zelest.github.io/privacy.html) détaille l'utilisation de Google Drive et les possibilités de suppression ou de révocation des autorisations.

## État du projet

| Élément | État |
|---|---|
| Sauvegarde locale Proxmox de Vaultwarden | ✅ Configurée et testée |
| Site GitHub Pages | ✅ En place |
| Application OAuth Google | 🟡 En production, validation en attente |
| Connexion Rclone à Google Drive | 🔧 En cours |
| Sauvegardes Restic chiffrées | 📋 À mettre en place |
| Automatisation et test de restauration distante | 📋 À réaliser |

**Note :** l'architecture de sauvegarde distante est en cours de mise en place. Elle ne sera considérée comme opérationnelle qu'après validation des sauvegardes et d'une restauration.

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `index.html` | Page d'accueil |
| `privacy.html` | Politique de confidentialité |
| `styles.css` | Design sombre style Obsidian |
| `google*.html` | Vérification Google Search Console |
| `README.md` | Présentation et fonctionnement du projet |

Le dépôt GitHub est public uniquement pour héberger le site de présentation. Il ne contient aucune donnée sensible de l'infrastructure privée.

## Technologies

- [Vaultwarden](https://github.com/dani-garcia/vaultwarden) — Gestionnaire de mots de passe auto-hébergé
- [Proxmox VE](https://www.proxmox.com/) — Hébergement et sauvegardes locales
- [Restic](https://restic.net/) — Sauvegardes chiffrées et versionnées
- [Rclone](https://rclone.org/) — Transfert vers Google Drive
- [Google Drive](https://drive.google.com/) — Stockage distant
- [GitHub Pages](https://pages.github.com/) — Hébergement du site de présentation

---

*Blackwall Lab Backup est un projet personnel, sans affiliation avec Google, Restic, Rclone ou Vaultwarden.*
