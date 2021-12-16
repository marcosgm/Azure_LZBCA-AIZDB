# Azure_LZBCA-AIZDB

[![IaC](https://app.soluble.cloud/api/v1/public/badges/7941c1e0-7b55-45cf-864c-a7ecb373ddbb.svg)](https://app.soluble.cloud/repos/details/github.com/marcosgm/azure_lzbca-aizdb)  [![CIS](https://app.soluble.cloud/api/v1/public/badges/a3fbdfcc-47e2-4895-b5a9-c7ff0d314ac5.svg)](https://app.soluble.cloud/repos/details/github.com/marcosgm/azure_lzbca-aizdb)  [![HIPAA](https://app.soluble.cloud/api/v1/public/badges/d97224a5-c212-4bbe-b33e-34b9cdf19da9.svg)](https://app.soluble.cloud/repos/details/github.com/marcosgm/azure_lzbca-aizdb)  
Azure Landing Zone Base Cloud Architecture - Architecture infonuagique zone d'atterrissage de base

This initiative is a contribution to the GC Accelerators.

These tools and IaC (Infrastructure as Code) enable the Government of Canada's Cloud First direction and support for the GC Digital Standards.

The users of this initiative will be Government of Canada employees deploying cloud-based workloads.

# Background

The Azure Landing Zone Base Cloud Architecture **(LZBCA)** is an initiative that is led by Cloud Product Management & Services - Research & Development team. 

The Azure LZBCA is a fully functional Virtual Data Centre (VDC) with the necessary configuration to meet the 30-Day Guardrails (technical only) and many of the 90-Day guardrails through Infrastructure as Code (IaC). It aligns with Cloud Usage Profile 3, with a future design for Cloud Usage Profiles 5 & 6.� We will be starting our Security Assessment (SA) on the environment in June 2020. 
  
* For Network details See [Network Architecture](Network/README.md)
* For Routing details See [Routing and Flow Control Overview](Network/Routing_Overview.md)
* For Application Dataflow details see [Application Dataflow - HA and AzLB](Network/Application_Dataflow_-_HA_and_AzLB.md)

It has been designed to enable departments to leverage and quickly deploy an Azure Landing Zone that aligns with a departments naming standards and IP blocks.

Development of the Azure LZBAC will continue to add functionality for components such as: SCED, AD, RBAC and etc., this development will move forward in parallel with the SA process. For a complete list of current and future development "Available Today" and "Future Releases" below.

______________________


## How to Contribute

See [CONTRIBUTING.md](CONTRIBUTING.md)
Contact [ssc.azurelzbca-azureaizdb.spc@canada.ca](mailto:ssc.azurelzbca-azureaizdb.spc@canada.ca)

## License

Unless otherwise noted, the source code of this project is covered under Crown Copyright, Government of Canada, and is distributed under the [MIT License](LICENSE).

The Canada wordmark and related graphics associated with this distribution are protected under trademark law and copyright law. No permission is granted to use them outside the parameters of the Government of Canada's corporate identity program. For more information, see [Federal identity requirements](https://www.canada.ca/en/treasury-board-secretariat/topics/government-communications/federal-identity-requirements.html).

______________________

# Code Generation Pipeline

The code pipeline begin with an VDC input configuration spread sheet, this is used to build a control file that is ingested by a PowerShell script to create all the necessary Terraform �*.tf� files required to deploy a VDC.

![Diagram](Resources/code-pipeline.png)

## VDC Configuration Spreadsheet defines the following values
Resource groups, virtual and sub networks, peering and user defined routing, Virtual machines + availability sets, Windows domain controller, Fortinet HA firewall, F5/Azure HA load balancer, Azure SDN app, Log analytics Workspace, NICs + temporary public Ips [config & licensing], network security groups, Azure security center [+ subscription activation]

# Future Development Roadmap

![Diagram](Resources/azure-roadmap.png)

# **Available Today**
1. Azure LZBCA r2b = fully functional VDC
   - Core Security Infrastructure
     - F5
       - HA pair (Active/Passive)
       - Outbound Internet NAT
       - Application Delivery (LTM)
         - SSL Offload
       - Remote Access (APM)
         - Access Portal
         - RDS Proxy 
     - FortiGate
       - VM-08 HA pair (Active/Passive)
       - Prod and Dev separation using vDOMs
       - Flow Control
       - URL Whitelist
       - IPS/IDS
       - Anti-Malware
       - SSL Inspection
   - ITSG-22 Zoning
     - Management Restricted Zone (MRZ)
     - Management Access Zone (MAZ)
     - Public Access Zone (PAZ) > Prod & Dev
     - Operation Zone (OZ) > Prod & Dev
     - Data Restricted Zone (RZ) > Prod & Dev
     - Application Restricted Zone (RZ) > Prod & Dev
     - FE Private Restricted Zone (RZ) > Prod & Dev
2. Managed Service available to help deploy an Azure Landing Zone with aligned naming standards and IP blocks.
3. Azure Naming and Tagging Standards
4. 30-Day Guardrail Implementation Guide
5. 30-Day Guardrails Applied (Technical GR only)
6. Reporting tool
7. Deploys a Local Active Directory (azure.local)


# **Future Releases**
1. 30 Day Guardrail Compliance Automation Tool (r2c)
2. Integrate F5 into pipeline (r2c)
3. Modularize Terraform Deployement
   - F5 (r2c)
   - FortiGate (r2c)
   - Core Infrastructure (r2c)
   - Bolt on Components
     - Subscription (r2d)
     - Resource Group (r2d)
     - vNets/sNets (r2d)
     - Key Vault (r2d)
4. IaaS/PaaS Guardrail Compliance Automation
   - 30-Day Guardrails (r2c)
   - 90-Day Guardrails (r2d)
   - 180-Day Guardrails (r2d)
5. Separate FortiGate HA pairs for Prod and Dev (r2c)
6. SCED Connectivity / Cloud Usage Profile 5 & 6 (r2d)
7. Active Directory Domain Services - Ground <-> Cloud (r2d)
8. ATO - Cloud PBMM Security Profile (Technical Controls Only)
9. F5 authentication to used local Active Directory
10. Hardening of all infrastructure
11. High-Level Governance Framework 

______________________

# Current Release Limitations

Azure LZBCA release 2b has a couple limitations when using the pipeline to generate new *.TF files to create a custom VDC, these limitations are:

1. The F5 code in this repository is fully functional, however it did not go through the pipeline and was manually configure via IaC. This will be rectified for our r2c release.  If you require to customize a deployment (integrate your naming standard and IP blocks) before our next release, we suggest to leverage our managed service to help with the process.

2. There are also a list of pre and post deployment steps that are required, these are available here See [LZ Deployment Steps](Terraform/README.md).  We plan to automate some of these steps in future

______________________

# Notes

Post deployment tasks:

**Must change all default passwords and userids for all accounts.**

______________________

# Azure_LZBCA-AIZDB
Azure Cloud Landing Zone Base Cloud Architecture - Architecture infonuagique zone d'atterrissage de base

Cette initiative est une contribution aux acc�l�rateurs du GC.

Ces outils et IaC (Infrastructure as Code) permettent au gouvernement du Canada d'orienter et de soutenir les normes num�riques du GC.

Les utilisateurs de cette initiative seront des employ�s du gouvernement du Canada qui d�ploieront des charges de travail en infonuagique.

# Contexte

L'AIZDB est une initiative dirig�e par la direction des services et de la gestion des produits infonuagiques- �quipe de recherche et d�veloppement.

L�AIZDB est un centre de donn�es virtuel (CDV) enti�rement fonctionnel dot� de toutes les composantes n�cessaires pour rencontrer les garde-fous de 30 jours (aspects techniques) ainsi que plusieurs des garde-fous de 90 jours via une infrastructure d�ployable par Code (IaC). Il s'aligne sur le profil d'utilisation infonuagique 3 avec une conception future qui tiens compte des profils d'utilisation infonuagique 5 et 6. Nous commencerons notre �valuation de la s�curit� (SA) sur l'environnement en juin 2020.

Il a �t� con�u pour permettre aux partenaires de d�ployer rapidement une zone d'atterrissage Azure qui s'aligne sur les normes de d�nomination et les blocs d�addresses IP d'un partenaire.

Le d�veloppement d'AAIZDB continuera � ajouter des fonctionnalit�s pour des composantes tels que: SCED, AD, RBAC et etc.. Ce d�veloppement se fera en parall�le avec le processus d��valuation de la s�curit�. Pour une liste compl�te des fonctionnalit�s en d�veloppements actuels et futurs, voir les sections "Available Today � Disponible auhourd�hui" et "Future Releases � Prochaines versions" ci-dessous.

______________________


## Comment contribuer

Voir [CONTRIBUTING.md](CONTRIBUTING.md)
Contactez [ssc.azurelzbca-azureaizdb.spc@canada.ca](mailto:ssc.azurelzbca-azureaizdb.spc@canada.ca)

## Licence

Sauf indication contraire, le code source de ce projet est couvert par le droit d'auteur de la Couronne, gouvernement du Canada, et est distribu� sous la [Licence MIT] (LICENCE).

Le mot-symbole Canada et les graphiques associ�s � cette distribution sont prot�g�s par le droit des marques et le droit d'auteur. Aucune autorisation n'est accord�e pour les utiliser en dehors des param�tres du programme d'identit� corporative du gouvernement du Canada. Pour plus d'informations, voir [Exigences f�d�rales en mati�re d'identit�] (https://www.canada.ca/fr/treasury-board-secretariat/topics/government-communications/federation-identity-requirements.html).

______________________

# Pipeline de g�n�ration de code

Le pipeline de code commence par une feuille de calcul de configuration d'entr�e VDC, qui est utilis�e pour cr�er un fichier de contr�le qui est ing�r� par un script PowerShell pour cr�er tous les fichiers Terraform �* ??.tf� n�cessaires pour d�ployer un VDC.

![Diagram](Resources/code-pipeline.png)

## VDC Configuration Spreadsheet d�finit les valeurs suivantes
Groupes de ressources, r�seaux virtuels et sous-r�seaux, homologation et routage d�fini par l'utilisateur, machines virtuelles + ensembles de disponibilit�, contr�leur de domaine Windows, pare-feu Fortinet HA, �quilibreur de charge F5 / Azure HA, application Azure SDN, espace de travail d'analyse des journaux, cartes r�seau + Ips publiques temporaires [config et licences], groupes de s�curit� r�seau, Azure Security Center [+ activation de l'abonnement]

# Feuille de route pour le d�veloppement futur

![Diagram](Resources/azure-roadmap.png)

# **Disponible aujourd'hui**
1. Azure LZBCA r2b = VDC enti�rement fonctionnel
   - Infrastructure de s�curit� principale
     - F5
       - Paire HA (active / passive)
       - NAT Internet sortant
       - Livraison d'application (LTM)
         - D�chargement SSL
       - Acc�s � distance (APM)
         - Portail d'acc�s
         - Proxy RDS
     - FortiGate
       - Paire VM-08 HA (active / passive)
       - S�paration Prod et Dev � l'aide de vDOM
       - Contr�le de flux
       - Liste blanche d'URL
       - IPS / IDS
       - Anti-Malware
       - Inspection SSL
   - Zonage ITSG-22
     - Zone � gestion restreinte (MRZ)
     - Zone d'acc�s � la gestion (MAZ)
     - Zone d'acc�s public (PAZ)> Prod & Dev
     - Zone d'op�ration (OZ)> Prod & Dev
     - Zone restreinte de donn�es (RZ)> Prod & Dev
     - Zone d'application restreinte (RZ)> Prod & Dev
     - FE Zone priv�e restreinte (RZ)> Prod & Dev
2. Service g�r� disponible pour aider � d�ployer une zone d'atterrissage Azure avec des normes de d�nomination align�es et des blocs IP.
3. Normes de nommage et d'�tiquetage Azure
4. Guide de mise en �uvre de garde-corps de 30 jours
5. Garde-corps de 30 jours appliqu�s (GR technique uniquement)
6. Outil de rapports
7. D�ploie un r�pertoire AD local (azure.local)

# ** Versions futures **
1. Outil d'automatisation de la conformit� des garde-corps de 30 jours (r2c)
2. Int�grer F5 dans le pipeline (r2c)
3. Modulariser le d�ploiement de Terraform
   - F5 (r2c)
   - FortiGate (r2c)
   - Infrastructure principale (r2c)
   - Composants boulonn�s
     - Abonnement (r2d)
     - Groupe de ressources (r2d)
     - vNets / sNets (r2d)
     - Key Vault (r2d)
4. Automatisation de la conformit� IaaS / PaaS Guardrail
   - Garde-corps de 30 jours (R2C)
   - Garde-corps 90 jours (R2D)
   - Garde-corps de 180 jours (R2D)
5. S�parer les paires FortiGate HA pour Prod et Dev (r2c)
6. Connectivit� SCED / Profil d'utilisation infonuagique 5 et 6 (r2d)
7. Services de domaine Active Directory - Ground <-> Cloud (r2d)
8. ATO - Profil de s�curit� Cloud PBMM (contr�les techniques uniquement)
9. Authentification F5 pour Active Directory local utilis�
10. Durcissement de toutes les infrastructures
11. Cadre de gouvernance de haut niveau

# Remarques

T�ches post-d�ploiement:
Doit changer tous les mots de passe et ID utilisateur par d�faut pour tous les comptes.

______________________

# Limites actuelles des versions

Azure AIZDB version 2b a quelques limitations lors de l'utilisation du pipeline pour g�n�rer de nouveaux fichiers * .TF pour cr�er un VDC personnalis�, ces limitates sont les suivantes:

1. Le code F5 dans ce r�f�rentiel est enti�rement fonctionnel, mais il n'est pas pass� par le pipeline et a �t� configur� manuellement via IaC. Cela sera corrig� pour notre version r2c. Si vous souhaitez personnaliser un d�ploiement (int�grer votre norme de d�nomination et vos blocs IP) avant notre prochaine version, nous vous sugg�rons de tirer parti de notre service g�r� pour vous aider dans le processus.

2. Il existe �galement une liste des �tapes de pr� et post d�ploiement qui sont requises, celles-ci sont disponibles ici "ajouter un lien aux �tapes". Nous pr�voyons automatiser certaines de ces �tapes dans le future.





