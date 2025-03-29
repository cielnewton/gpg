cat << EOF > README.md
# 🔐 Utilisation de GPG (gpg2) – Création et chiffrement de messages

Ce guide explique comment générer une paire de clés GPG, partager sa clé publique, importer celle d’un correspondant, et chiffrer/déchiffrer des messages.

---

## ✅ Prérequis

- Système : Linux (Ubuntu ou dérivé)
- GPG installé : `gnupg2`

```bash
sudo apt update
sudo apt install gnupg2
```

---

## 1️⃣ Générer une paire de clés

```bash
gpg --full-generate-key
```

**Options recommandées :**
- Type : RSA and RSA
- Taille : 4096 bits
- Expiration : selon tes besoins
- Identité : nom + e-mail
- Mot de passe : sécurisé

---

## 2️⃣ Lister ses clés

```bash
gpg --list-keys
```

Tu verras ton UID (nom + e-mail) et ton **ID de clé** (8 ou 16 caractères hexadécimaux).

---

## 3️⃣ Exporter ta clé publique

```bash
gpg --armor --export ton_email@example.com > ma_cle_publique.asc
```

➡️ Ce fichier peut être envoyé à ton correspondant pour qu’il puisse te chiffrer des messages.

---

## 4️⃣ Envoyer ta clé sur un serveur public

```bash
gpg --keyserver keyserver.ubuntu.com --send-keys TON_ID_DE_CLE
```

Exemple :

```bash
gpg --keyserver keyserver.ubuntu.com --send-keys C0CC8F0C1F41CEF
```

---

## 5️⃣ Importer une clé publique reçue

```bash
gpg --import cle_correspondant.asc
```

Ou rechercher une clé sur un serveur :

```bash
gpg --keyserver keyserver.ubuntu.com --search-keys email@domaine.com
```

Puis tape `1` pour importer la bonne clé.

---

## 6️⃣ Chiffrer un message ou un fichier

### 📄 Exemple avec un fichier texte :

```bash
gpg --armor --encrypt -r destinataire@email.com message.txt
```

➡️ Résultat : `message.txt.asc` (lisible uniquement par le destinataire)

---

## 7️⃣ Déchiffrer un message

```bash
gpg --decrypt message.txt.asc
```

---

## 8️⃣ (Optionnel) Signer un fichier

```bash
gpg --armor --sign fichier.txt
```

Pour **signer et chiffrer en même temps** :

```bash
gpg --armor --encrypt --sign -r destinataire@email.com message.txt
```

---

## 🧼 Bonnes pratiques

- Ne jamais partager ta **clé privée**
- Toujours protéger ta clé par mot de passe
- Publier uniquement ta **clé publique**
- Vérifier les signatures si on te fournit un fichier signé

---

## 📂 Répertoire par défaut des clés

```bash
~/.gnupg/
```

---

## 🔚 Exemple complet

```bash
# 1. Génération de clé
gpg --full-generate-key

# 2. Export de la clé publique
gpg --armor --export mon@mail.fr > pubkey.asc

# 3. Envoi sur serveur de clés
gpg --keyserver keyserver.ubuntu.com --send-keys MON_ID_DE_CLE

# 4. Import de la clé du destinataire
gpg --import cle_recue.asc

# 5. Chiffrement d’un fichier
gpg --armor --encrypt -r destinataire@mail.fr message.txt

# 6. Déchiffrement
gpg --decrypt message.txt.asc
```
EOF
