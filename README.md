cat << 'EOF' > README.md
# 🔐 Utilisation de GPG (gpg2) – Création et chiffrement de messages

Ce guide explique comment générer une paire de clés GPG, partager sa clé publique, importer celle d’un correspondant, et chiffrer/déchiffrer des messages.

---

## ✅ Prérequis

- Système : Linux (Ubuntu ou dérivé)
- GPG installé : gnupg2

Commandes :

sudo apt update
sudo apt install gnupg2

---

## 1️⃣ Générer une paire de clés

Commande :

gpg --full-generate-key

Options recommandées :
- Type : RSA and RSA
- Taille : 4096 bits
- Expiration : selon tes besoins
- Identité : nom + e-mail
- Mot de passe : sécurisé

---

## 2️⃣ Lister ses clés

Commande :

gpg --list-keys

Tu verras ton UID (nom + e-mail) et ton ID de clé.

---

## 3️⃣ Exporter ta clé publique

Commande :

gpg --armor --export ton_email@example.com > ma_cle_publique.asc

---

## 4️⃣ Envoyer ta clé sur un serveur public

Commande :

gpg --keyserver keyserver.ubuntu.com --send-keys TON_ID_DE_CLE

Exemple :

gpg --keyserver keyserver.ubuntu.com --send-keys C0CC8F0C1F41CEF

---

## 5️⃣ Importer une clé publique reçue

Commande :

gpg --import cle_correspondant.asc

Ou rechercher une clé sur un serveur :

gpg --keyserver keyserver.ubuntu.com --search-keys email@domaine.com

---

## 6️⃣ Chiffrer un message ou un fichier

Exemple avec un fichier texte :

gpg --armor --encrypt -r destinataire@email.com message.txt

Résultat : message.txt.asc

---

## 7️⃣ Déchiffrer un message

Commande :

gpg --decrypt message.txt.asc

---

## 8️⃣ (Optionnel) Signer un fichier

Signer :

gpg --armor --sign fichier.txt

Signer + chiffrer :

gpg --armor --encrypt --sign -r destinataire@email.com message.txt

---

## 🧼 Bonnes pratiques

- Ne jamais partager ta clé privée
- Toujours protéger ta clé par mot de passe
- Publier uniquement ta clé publique
- Vérifier les signatures si on te fournit un fichier signé

---

## 📂 Répertoire par défaut des clés

~/.gnupg/

---

## 🔚 Exemple complet

gpg --full-generate-key  
gpg --armor --export mon@mail.fr > pubkey.asc  
gpg --keyserver keyserver.ubuntu.com --send-keys MON_ID_DE_CLE  
gpg --import cle_recue.asc  
gpg --armor --encrypt -r destinataire@mail.fr message.txt  
gpg --decrypt message.txt.asc

EOF
