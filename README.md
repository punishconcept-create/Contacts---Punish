# Contacts Punish · version installable

Cette version reprend l'interface de Contacts Bizouk dans une PWA installable. Elle appelle les mêmes fonctions du **même projet Apps Script** via l'API Apps Script. Les données des imports restent dans le Google Sheet identifié par `DB_ID` du script existant. Ne créez pas un nouveau projet Apps Script et ne relancez pas `setup` dans un nouveau projet : vous perdriez le lien avec l'historique.

## Configuration nécessaire

1. Dans Google Cloud, créer ou sélectionner un **projet standard** et l'associer au projet Apps Script actuel dans ses paramètres. Activer Apps Script API, People API et Drive API dans ce projet. Changer le projet Cloud peut demander de réautoriser le script.
2. Dans le même projet Cloud, configurer l'écran de consentement OAuth pour un usage personnel et ajouter le compte Google propriétaire des contacts comme utilisateur test si l'application est en mode test. Créer un **ID client OAuth de type application Web**. Renseigner l'origine HTTPS exacte du site installable dans « Origines JavaScript autorisées ».
3. Remplacer `appsscript.json` du projet Apps Script actuel par celui fourni ici (il ajoute `executionApi` et conserve `webapp`). Déployer ce **même projet** comme « Exécutable d'API », accessible à « Moi uniquement ». Conserver aussi son déploiement Web actuel jusqu'à la validation de la nouvelle interface.
4. `config.js` contient déjà l'ID client OAuth et l'ID du déploiement « Exécutable d'API ». Il ne contient aucun secret.
5. Héberger `index.html`, `config.js`, `manifest.webmanifest`, `sw.js` et les deux PNG **sur une origine HTTPS** (par exemple un site Pages déjà maîtrisé). Ouvrir le site dans Chrome Android, se connecter au même compte Google, vérifier un import existant en lecture avant tout nouvel import, puis utiliser « Installer l'application ».

Les jetons OAuth ne sont conservés qu'en mémoire. La connexion Google peut donc être redemandée après la fermeture de l'application. Les fichiers Bizouk sélectionnés sont transmis au script existant et ne sont pas mis dans le cache du service worker. Le mode hors ligne sert seulement à afficher la coque ; les contacts nécessitent le réseau.

**État :** la configuration Cloud et le déploiement API ont été faits le 29 septembre 2026. Les fichiers du site doivent encore être hébergés et l'application testée sur le compte Google réel. Ne publiez aucun secret OAuth dans `config.js`.
