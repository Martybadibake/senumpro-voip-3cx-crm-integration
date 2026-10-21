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

<img width="1896" height="745" alt="17-3cx-microsoft365-integration-status" src="https://github.com/user-attachments/assets/e107e3f4-699e-42e0-a751-381248d5412c" />
L’interface 3CX confirme que l’intégration Microsoft 365 est configurée et que les notifications sont synchronisées. Cette étape valide l’état de l’intégration affiché par la plateforme.

<img width="1653" height="845" alt="18-dynamics365-crm-contact-lookup-test" src="https://github.com/user-attachments/assets/b4a11fa0-9a88-42c2-91d7-721216dc450a" />
Un test de recherche CRM est exécuté à partir d’un numéro de téléphone. La plateforme retrouve une fiche de contact dans Dynamics 365, ce qui confirme le fonctionnement de la recherche pour ce numéro.

<img width="1836" height="926" alt="19-dynamics365-crm-second-contact-test" src="https://github.com/user-attachments/assets/c6e24a23-c616-4263-ba0f-4c16639f2f73" />

Un second test est réalisé avec un autre numéro de téléphone. Le résultat confirme que la recherche CRM peut retrouver une autre fiche de contact.

<img width="1702" height="852" alt="20-3cx-dynamics365-successful-call-test" src="https://github.com/user-attachments/assets/9a435e3c-4937-44b8-abb2-a631757b782f" />

Cette capture documente un test d’appel associé à l’intégration CRM. Elle complète les tests de recherche en illustrant le fonctionnement de la téléphonie avec les données de contact.
<img width="1906" height="701" alt="21-dynamics365-contact-call-activity" src="https://github.com/user-attachments/assets/d2aca1ee-60f3-4bd2-8cf8-10ceb46e339f" />

Une activité liée à un appel 3CX apparaît dans la chronologie d’une fiche de contact Dynamics 365. Cette preuve montre que les informations relatives à l’appel peuvent être consignées dans le CRM.

Étape 7 — Sauvegarde et surveillance
<img width="1842" height="629" alt="22-3cx-event-logs-and-troubleshooting" src="https://github.com/user-attachments/assets/597e2fe5-72ce-4c28-ab63-d9cf11da60c8" />

Le journal des événements présente les événements système, les changements d’état du trunk SIP et du SBC, ainsi que des messages d’erreur. Ces informations sont utiles pour analyser les incidents et vérifier la stabilité des services. Les erreurs visibles rappellent qu’une surveillance régulière reste nécessaire.

<img width="1739" height="728" alt="23-3cx-manual-backup" src="https://github.com/user-attachments/assets/a13e7cfb-8833-40b6-b918-8c1da986f7f1" />

Une sauvegarde de la configuration 3CX est présente dans l’interface. Cette fonctionnalité permet de conserver une copie de la configuration pour faciliter une restauration en cas de problème.

<img width="1633" height="455" alt="24-3cx-automatic-backup-status" src="https://github.com/user-attachments/assets/1aa75ff9-e3b9-47ef-afbe-17b03a3d7341" />
Cette capture présente l’état de la sauvegarde automatique. Elle permet de documenter le mécanisme de sauvegarde configuré et son état au moment de la capture.

4. Résultats obtenus
Le projet a permis de mettre en place un environnement de téléphonie IP reposant sur 3CX, avec un SBC sous Debian 12 et un téléphone Yealink SIP-T46U.

Les tests réalisés ont notamment permis de vérifier :
- le fonctionnement du service SBC sous Debian ;
- la réponse HTTPS de la plateforme 3CX depuis le serveur Debian ;
- la présence des utilisateurs et des extensions dans 3CX ;
- la configuration du trunk SIP et des règles d’appels sortants ;
- l’authentification de l’application Microsoft et les autorisations associées ;
- la recherche de contacts dans Dynamics 365 ;
- l’apparition d’une activité d’appel dans la chronologie d’un contact ;
- la présence des fonctions de journalisation et de sauvegarde dans 3CX.
Les captures constituent des preuves des étapes réalisées et des résultats observés au moment des tests. Elles ne signifient pas, à elles seules, que tous les scénarios possibles ont été validés.
5. Conclusion
Ce projet m’a permis de mettre en pratique plusieurs compétences en administration système et réseau, en téléphonie IP et en intégration de services cloud.

La réalisation du laboratoire m’a amené à configurer les utilisateurs et les téléphones, à mettre en service un SBC sous Debian 12, à connecter un fournisseur SIP et à intégrer 3CX avec Microsoft Dynamics 365 et Microsoft 365.

Les tests de recherche CRM et la présence d’une activité d’appel dans Dynamics 365 démontrent l’intérêt de relier une solution de téléphonie à un outil de gestion de la relation client. La vérification du service Debian, les journaux et les sauvegardes illustrent également l’importance de la supervision et de la continuité de service.

Ce laboratoire constitue une base concrète pour mon portfolio professionnel en administration système, téléphonie IP et intégration de services informatiques. Il pourra être enrichi par des tests complémentaires de résilience, de restauration des sauvegardes et de validation des appels dans différents scénarios.
6. Sécurité et bonnes pratiques
Les captures publiées dans le dépôt GitHub doivent être vérifiées avant leur diffusion. Les mots de passe, jetons OAuth, identifiants sensibles, adresses IP publiques et données personnelles qui ne sont pas nécessaires à la démonstration doivent être masqués.

Le projet présente les éléments techniques utiles à la compréhension du laboratoire sans publier les secrets d’authentification ni les informations confidentielles de l’environnement.








