# Déploiement et intégration d’une solution de téléphonie IP avec 3CX
Projet de téléphonie IP avec 3CX V20, SBC sous Debian 12, téléphone Yealink, trunk SIP Callcentric et intégration Microsoft Dynamics 365 et Microsoft 365. Configuration, tests, dépannage et documentation technique
1. Présentation du projet
Ce projet consiste à mettre en place et à tester une solution de téléphonie IP avec 3CX, un téléphone physique Yealink SIP-T46U, un serveur 3CX SBC sous Debian 12 et un fournisseur de téléphonie SIP, Callcentric.

Le projet comprend également l’intégration de Microsoft Dynamics 365 pour associer les appels aux fiches de contacts du CRM, ainsi que l’intégration de Microsoft 365.

L’objectif est de développer un environnement fonctionnel qui illustre des compétences en administration système, en téléphonie IP, en configuration des postes utilisateurs, en intégration applicative et en dépannage.

2. Environnement technique

- Téléphonie IP : 3CX V20, hébergé par 3CX.
- Système d’exploitation : Debian 12 pour le SBC.
- Téléphone physique : Yealink SIP-T46U.
- Fournisseur SIP : Callcentric.
- CRM : Microsoft Dynamics 365.
- Services Microsoft : Microsoft Entra ID et Microsoft 365.

3. Réalisation du projet
Étape 1 — Mise en service de 3CX et du SBC
<img width="1911" height="738" alt="01-3cx-yealink-sbc-registration" src="https://github.com/user-attachments/assets/b92af28b-f07a-49f0-892d-f0129140dfe0" />
Cette capture présente l’association du téléphone Yealink à l’environnement 3CX. Elle permet de vérifier que le poste est identifié dans la plateforme et associé à un SBC.

<img width="1470" height="956" alt="02-debian-sbc-service-status" src="https://github.com/user-attachments/assets/fcb2954b-3740-433c-9e99-14aa08586b2f" />

Le serveur Debian 12 hébergeant le SBC est vérifié à l’aide de commandes système et réseau. Le service 3cxsbc est actif et configuré pour démarrer automatiquement. Le test HTTPS retourne également le code HTTP 200, confirmant que le serveur 3CX répond à cette requête depuis Debian.
<img width="1916" height="869" alt="03-3cx-system-dashboard" src="https://github.com/user-attachments/assets/bbb677ef-d790-4601-a097-a01ed936ae45" />
Le tableau de bord présente les informations générales de la plateforme 3CX, notamment la version, le nom de domaine, les extensions et les paramètres de téléphonie. Cette vue sert de point de départ pour vérifier l’état général du système.
Étape 2 — Configuration des utilisateurs et des téléphones
<img width="1897" height="880" alt="04-3cx-user-extensions-overview" src="https://github.com/user-attachments/assets/a0f1262d-01ea-4f1b-8e7d-b4eddd6f5146" />
La liste des utilisateurs permet de visualiser les extensions créées dans 3CX et leur association aux utilisateurs. Cette configuration facilite la gestion des postes et des comptes de téléphonie.
<img width="1904" height="682" alt="05-3cx-department-configuration" src="https://github.com/user-attachments/assets/efdfbdc1-2411-45c8-b072-8ee903dd0acd" />
Le département par défaut regroupe les utilisateurs et permet de définir les autorisations liées à leur rôle. Cette organisation contribue à structurer l’administration de la téléphonie.
<img width="1825" height="870" alt="06-yealink-sip-t46u-configuration" src="https://github.com/user-attachments/assets/1f82ca25-a762-4378-a89e-23d872000094" />
La configuration du Yealink SIP-T46U présente les paramètres du téléphone associés à l’extension 101. Cette étape permet de vérifier le modèle sélectionné et les informations de provisionnement du poste.
<img width="660" height="1413" alt="07-3cx-mobile-incoming-call" src="https://github.com/user-attachments/assets/eb24d7de-bac4-477d-9d65-1ec30608683f" />

Cette capture montre un appel entrant sur l’application mobile 3CX. Elle illustre la réception d’un appel sur un terminal mobile.
<img width="660" height="1354" alt="08-3cx-mobile-contacts-and-extensions" src="https://github.com/user-attachments/assets/d8101e1b-0357-405b-9a04-52ac06966f49" />

L’application mobile affiche les contacts et les extensions disponibles. Cette vue permet de vérifier l’accès aux utilisateurs depuis le client mobile 3CX.

Étape 3 — Configuration de la téléphonie externe
<img width="1821" height="692" alt="09-callcentric-sip-trunk-configuration" src="https://github.com/user-attachments/assets/c805dfd6-e5f4-4106-93bc-4dc339375386" />
Le trunk SIP Callcentric est visible dans la configuration Voix et Chat de 3CX. Il permet de relier la plateforme à un fournisseur de téléphonie externe pour acheminer les appels entrants et sortants.

<img width="1904" height="661" alt="10-3cx-outbound-calling-rule" src="https://github.com/user-attachments/assets/899c25e2-6ca5-41bd-86cb-e48f7b14c11e" />

La règle de sortie associe les appels concernés au trunk Callcentric. Elle détermine comment les numéros composés sont orientés vers le fournisseur SIP.
Étape 4 — Enregistrement de l’application Microsoft Entra ID
<img width="1876" height="918" alt="11-entra-dynamics365-app-registration" src="https://github.com/user-attachments/assets/1f64e20c-ae25-42f2-a8c4-25b2aefa111e" />

Une application nommée « 3CX Dynamics Integration » est créée dans Microsoft Entra ID. Cette application sert à établir l’authentification nécessaire à l’intégration entre 3CX et Dynamics 365

<img width="1891" height="874" alt="12-entra-app-registration-confirmation" src="https://github.com/user-attachments/assets/838a6582-7669-42df-aaae-1b9f9badc70b" />
Cette capture présente l’application enregistrée dans Entra ID et ses principales informations de configuration. Elle permet de confirmer la création de l’application utilisée pour l’intégration.

<img width="1901" height="946" alt="13-entra-api-permissions-configuration" src="https://github.com/user-attachments/assets/aa419d5f-4539-45d2-8a8f-6e5cb265ae87" />
Les autorisations nécessaires sont ajoutées aux API Microsoft. Elles comprennent l’autorisation déléguée user_impersonation pour Dynamics CRM et User.Read pour Microsoft Graph.

<img width="1904" height="796" alt="14-entra-api-permissions-review" src="https://github.com/user-attachments/assets/60708ae6-ac29-46c7-ae85-7be5c25ded6f" />
Les autorisations configurées sont vérifiées avant leur utilisation. Cette étape permet de contrôler les permissions demandées par l’application.

<img width="1440" height="519" alt="15-entra-admin-consent-granted" src="https://github.com/user-attachments/assets/6bb195fc-b348-4e6e-887a-237e15889ca3" />

Le consentement de l’administrateur est accordé pour les autorisations demandées. Cette validation permet à l’intégration de poursuivre son processus d’autorisation dans le tenant concerné.

Étape 5 — Intégration de Dynamics 365 et de Microsoft 365
<img width="1898" height="876" alt="16-3cx-dynamics365-crm-integration" src="https://github.com/user-attachments/assets/ae776968-c1c9-4bd4-ade3-097fbd0108d2" />

Le connecteur Microsoft Dynamics 365 est configuré dans 3CX. Les paramètres comprennent les informations de l’application, le tenant et le domaine CRM. L’autorisation OAuth permet d’établir la connexion entre les deux plateformes.


