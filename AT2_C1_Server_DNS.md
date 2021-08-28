
![cefim](https://metiersculture.fr/wp-content/uploads/2016/04/logo-cefim-tours.jpg)<br/>
*Cours 2021-2022*

---

# **ADMINISTATION RESEAU**

---

**Semaine 1**
1. DNS
2. DHCP
3. Web : HTTP + HTTPs
4. FTP + FTPs

**Semaine 2**
1. AD
2. WServer

<u>Deux protocoles essentiels</u> : [**BGP**](https://fr.wikipedia.org/wiki/Border_Gateway_Protocol) (protocole de routage, interco de routers) + **DNS** (protocole sur lequel se base tous les autres services)

---

# Table des matières

1. [Protocole DNS](#1)
    1. [Introduction](#2)
        1. [Domain Name System (ou DNS, système de noms de domaine)](#3)
        2. [Principe du DNS](#4)
        3. [Serveurs DNS racine](#5)
        4. [Qualified Domain Name](#6)
        5. [Hiérarchie du DNS](#7)
        6. [Résolution du nom par un hôte](#8)
        7. [Résolution Inverse](#9)
        8. [Les différents types d'enregistrements du DNS](#10)
        9. [Quelques Considérations Opérationnelles sur le DNS](#11)
        10. [Sécurité du DNS](#12)
    2. [Le DNS par Stéphane Bortzmeyer](#13)
    3. [Exercices](#14)

---

![logo1](https://kayamaga.com/wp-content/uploads/2019/07/DNS.jpg)

## Protocole DNS <a name="1"></a>

- Protocole le plus important pour TSSR
- Logiciel : [**BIND_9**](https://doc.ubuntu-fr.org/bind9) (sezvice DNS le plus utilisé)
- Logiciels bis : dig, nslookup...
- tout équipement connecté sur le web a besoin d'un nom qualifié (y compris routers)
- Au niveau DNS que l'on fait du meilleur filtrage
- Couche 7 OSI
- Fonctionne via [UNICODE](https://fr.wikipedia.org/wiki/Unicode)

Le Système de Nom de Domaine est un système distribué, hiérarchisé, robuste et pouvant être sécurisé qui à fait ses preuves.
Il constitue maintenant l'épine dorsale d'internet et des réseaux.
Beaucoup de services réseaux repose sur ce système et ne peuvent fonctionner sans le DNS (Serveur Mail, Serveur Ldap...)
Il facilite aussi beaucoup la vie des internautes qui préfère retenir www.google.fr 209.85.229.147, ils ne pourrait plus s'en passer. Les utilisateurs préfère d'ailleurs les noms en toute lettres au chiffre. Tout le monde fait sont propre "« DNS »" avec ses contact dans son téléphone portable.

### **Ressources web**

- [Neptunet : DNS](https://neptunet.fr/category/systeme/roles-et-services/dns/)
- [Neptunet : mise en pratique](https://neptunet.fr/dns-cache-windows/)
- [FrameIP](https://www.frameip.com/dns/)
- [Cisco](https://cisco.goffinet.org/ccna/services-infrastructure/protocole-resolution-noms-dns/)
- [Wikipedia](https://fr.wikipedia.org/wiki/Domain_Name_System)
- [OpenClassroom DNS](https://openclassrooms.com/fr/courses/857447-apprenez-le-fonctionnement-des-reseaux-tcp-ip/857163-le-service-dns)
- [Dernière RFC de 2019](https://datatracker.ietf.org/doc/html/rfc8499)
- [It-connect](https://www.it-connect.fr/chapitres/dns-presentation-et-definitions/)
- [Cours du CNAM](https://cefimeu-my.sharepoint.com/:b:/g/personal/rdelmas_cefim_eu/EWU-5P6Y069AoIY2zi18doQB8drMMJPGtTAekMqglq2TSg?e=nmakUJ)
- [Cloudflare](https://www.cloudflare.com/fr-fr/learning/dns/what-is-dns/)

### **Introduction** <a name="2"></a>

- Avant : juste fichier Host
- Ensuite : DNS


#### **Domain Name System (ou DNS, système de noms de domaine)** <a name="3"></a>

C'est un service permettant d'établir une **correspondance** entre une adresse IP et un nom de domaine et, plus généralement, de trouver une information à partir d'un nom de domaine. C'est un **système hiérarchisé**, il part d'un Domaine générale qui se divise en sous domaine.

> protocole DNS avant de se connecter au web <br/>
> système de correspondance entre humains et machines (binaires)<br/>
> avant on utilisait des *hostnames* mais problème avec la multiplication des hôtes<br/>
> www.google.fr.(=root, fin de l'arbre)<br/>

#### **Principe du DNS** <a name="4"></a>

Les ordinateurs connectés à un réseau IP, comme Internet, possèdent une adresse IP. Ces adresses sont numériques afin d'être plus facilement traitées par une machine. En IPv4, elles sont représentées sous la forme xxx.xxx.xxx.xxx, où xxx est un nombre variant entre 0 et 255 (en système décimal). En IPv6, les IP sont de la forme xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx, où x représente un caractère au format hexadécimal. Pour faciliter l'accès aux systèmes qui disposent de ces adresses, un mécanisme a été mis en place pour permettre **d'associer un nom à une adresse IP**, plus simple à retenir, appelé nom de domaine. Résoudre un nom de domaine consiste à trouver l'adresse IP qui lui est associée.

![schema](https://www.nameshield.com/wp-content/uploads/2020/03/DNS.png)

Les noms de domaines peuvent être également associés à d'autres informations que des adresses IP.

#### **Serveurs DNS racine** <a name="5"></a>

Il existe **13 serveurs racine**, nommés de ***A à M*** *.root-servers.net*. Ces serveurs sont gérés par douze organisations différentes : deux sont européennes, une japonaise et les neuf autres sont américaines. 10 de ces serveurs sont en réalité distribués dans le monde grâce à la technique anycast et 12 disposent d'une adresse IPv6. Grâce à anycast, plus de 900 serveurs répartis dans 50 pays du monde assurent ce service. Le serveur k reçoit par exemple de l'ordre de 20 000 requêtes par seconde.

Le DNS ne fournit pas de mécanisme pour découvrir la liste des serveurs racine, chacun des serveurs doit donc connaître cette liste au démarrage grâce à un encodage explicite. Cette liste est ensuite mise à jour en consultant l'un des serveurs indiqués. La mise à jour de cette liste est peu fréquente de façon à ce que les serveurs anciens continuent à fonctionner.

![root-servers](https://thehackernews.com/images/-Y_AY6xG9D3o/T3YI0b-vEeI/AAAAAAAAFdE/pF3lGt7qbVw/s640/DNS+root+servers.gif)


> Site qui recense tous les servers racines : https://root-servers.org/ <br/>
> Stats dispos (ex) : ipv4 > ipv6 + udp > tcp <br/>
> [IANA](https://www.iana.org/) -> [ICANN](https://www.icann.org/fr) (gère les noms de domaines (nom, .com, .fr...) et adresses IP (5 regional registar : RIPE, WIDE...)) <br/>


#### **Fully Qualified Domain Name (FQDN)** <a name="6"></a>

On entend par Fully qualified domain name (FQDN), ou Nom de domaine pleinement qualifié un **nom de domaine écrit de façon absolue**, y compris tous les domaines jusqu'au domaine de premier niveau (TLD), il est ponctué par un point final, par exemple *fr.wikipedia.org.*

La norme prévoit qu'un élément d'un nom de domaine (appelé label) ne peut dépasser 63 caractères, un FQDN ne pouvant dépasser 253 caractères.

> point (.), nom de domaine de 1er niveau (=TLD, org), nom de domaine de second niveau (wikipedia), nom de domaine de troisième niveau (fr)... <br/>

![schema](https://www.cloudflare.com/img/learning/dns/glossary/dns-root-server/dns-root-server.png)

> "www" = on cherche à joindre via le WorldWildWeb la machine... (on ne pointe que des machines/ressources, pas de servers) <br/>
> [TLD](https://fr.wikipedia.org/wiki/Domaine_de_premier_niveau) = [CCTLD](https://en.wikipedia.org/wiki/Country_code_top-level_domain) (*.fr*, country code) + [gTLD](https://en.wikipedia.org/wiki/Generic_top-level_domain) (nnom de domaine generic) <br/>
> jeux de noms de domaine : [domain hac](https://en.wikipedia.org/wiki/Domain_hack) <br/>

![TLD](https://audytorium.xyz/wp-content/uploads/2019/01/domeny.jpg)
- Liste des TLD disponible sur [Wikipedia](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains)


#### **Hiérarchie du DNS** <a name="7"></a>

Le système des noms de domaines consiste en une hiérarchie dont le sommet est appelé la racine. On représente cette dernière par un point. Dans un domaine, on peut créer un ou plusieurs sous-domaines ainsi qu'une délégation pour ceux-ci, c'est-à-dire une indication que les informations relatives à ce sous-domaine sont enregistrées sur un autre serveur. Ces sous-domaines peuvent à leur tour déléguer des sous-domaines vers d'autres serveurs.

![schema](https://upload.wikimedia.org/wikipedia/commons/thumb/9/91/Dns-raum.svg/400px-Dns-raum.svg.png)

Tous les sous-domaines ne sont pas nécessairement délégués. Les délégations créent des zones, c'est-à-dire des ensembles de domaines et leurs sous-domaines non délégués qui sont configurés sur un serveur déterminé. Les zones sont souvent confondues avec les domaines.

Les domaines se trouvant immédiatement sous la racine sont appelés domaine de premier niveau (TLD : Top Level Domain). Les noms de domaines ne correspondant pas à une extension de pays sont appelés des domaines génériques (gTLD), par exemple .org ou .com. S'ils correspondent à des codes de pays (fr, be, ch...), on les appelle ccTLD (country code TLD).

On représente un nom de domaine en indiquant les domaines successifs séparés par un point, les noms de domaines supérieurs se trouvant à droite. Par exemple, le domaine org. est un TLD, sous-domaine de la racine. Le domaine wikipedia.org. est un sous-domaine de .org.. Cette délégation est accomplie en indiquant la liste des serveur DNS associée au sous-domaine dans le domaine de niveau supérieur.

**Les noms de domaines sont donc résolus en parcourant la hiérarchie depuis le sommet et en suivant les délégations successives**, c'est-à-dire en parcourant le nom de domaine de droite à gauche.

Pour qu'il fonctionne normalement, un nom de domaine doit avoir fait l'objet d'une délégation correcte dans le domaine de niveau supérieur.

> ```tracert``` (permet de voir tous les sauts) <br/>
> Le gouvernement des USA gère sur la racine "." en 1998 <br/>
> ICAAN délégué par les USA pour la gestion quotidienne de la racine <br/>

#### **Résolution du nom par un hôte** <a name="8"></a>

Les hôtes n'ont qu'une connaissance limitée du système des noms de domaine. Quand ils doivent résoudre un nom, ils s'adressent à un ou plusieurs serveurs de noms dits récursifs, c'est-à-dire qui vont parcourir la hiérarchie DNS et faire suivre la requête à un ou plusieurs autres serveurs de noms pour fournir une réponse. Les adresses IP de ces serveurs récursifs sont souvent obtenues via DHCP ou encore configurés en dur sur la machine hôte. Les fournisseurs d'accès à Internet mettent à disposition de leurs clients ces serveurs récursifs. Il existe également des serveurs récursifs ouverts comme ceux de Google Public DNS ou OpenDNS et encore plus récemment Quad9 ou One.

Quand un serveur DNS récursif doit trouver l'adresse IP de fr.wikipedia.org, un processus itératif démarre pour consulter la hiérarchie DNS. Ce serveur demande aux serveurs DNS appelés serveurs racine quels serveurs peuvent lui répondre pour la zone org. Parmi ceux-ci, le serveur va en choisir un pour savoir quels serveurs sont capables de lui répondre pour la zone wikipedia.org. C'est un de ces derniers qui pourra lui donner l'adresse IP de fr.wikipedia.org. S'il se trouve qu'un serveur ne répond pas, un autre serveur de la liste sera consulté.

Pour optimiser les requêtes ultérieures, les serveurs DNS récursifs font aussi office de DNS cache : ils gardent en mémoire (cache) la réponse d'une résolution de nom afin de ne pas effectuer ce processus à nouveau ultérieurement. Cette information est conservée pendant une période nommée Time to live et associée à chaque nom de domaine.

Un nom de domaine peut utiliser plusieurs serveurs DNS. Généralement, les noms de domaines en utilisent au moins deux : un primaire et un secondaire. Il peut y avoir plusieurs serveurs secondaires.

L'ensemble des serveurs primaires et secondaires font autorité pour un domaine, c'est-à-dire que la réponse ne fait pas appel à un autre serveur ou à un cache. Les serveurs récursifs fournissent des réponses qui ne sont pas nécessairement à jour, à cause du cache mis en place. On parle alors de réponse ne faisant pas autorité (non-authoritative answer).

Cette architecture garantit au réseau Internet une certaine continuité dans la résolution des noms. Quand un serveur DNS tombe en panne, le bon fonctionnement de la résolution de nom n'est pas remis en cause dans la mesure où des serveurs secondaires sont disponibles.

![schema](https://d33wubrfki0l68.cloudfront.net/350a2c406907f37c5f12cfda3095b82cc150a30c/a2a00/assets/images/ccna/external/1126px-dns_iterations.svg.png)

> ```nslookup``` ([recherche d'infos dans le DNS](https://fr.wikipedia.org/wiki/Nslookup)) <br/>
> ```ipconfig/flushdns``` (vider le cache)<br/>
> ```ipconfig/displaydns``` (visualiser le cache)<br/>

> [**nslookup**](https://docs.microsoft.com/fr-fr/windows-server/administration/windows-commands/nslookup) sur Windows, [**dig**](https://fr.wikipedia.org/wiki/Dig_(programme_informatique)) sur Linux


#### Résolution Inverse <a name="9"></a>

![schema](https://images.ctfassets.net/plii0v5gbc4s/1Y1Z04UYBC4OIVcUYb2MIl/52f06f2598e7e7024a2a21957b12390a/reverse-dns-example.png)

Pour trouver le nom de domaine associé à une adresse IP, on utilise un principe semblable. Dans un nom de domaine, la partie la plus générale est à droite : org dans fr.wikipedia.org, le mécanisme de résolution parcourt donc le nom de domaine de droite à gauche. Dans une adresse IP, c'est le contraire : 213 est la partie la plus générale de 213.228.0.42. Pour conserver une logique cohérente, on inverse l'ordre des quatre termes de l'adresse et on la concatène au pseudo domaine in-addr.arpa. Ainsi, par exemple, pour trouver le nom de domaine de l'adresse IP 91.198.174.2, on résout 2.174.198.91.in-addr.arpa.

La déclaration inverse est importante sur les adresses IP publiques Internet puisque l'absence d'une résolution inverse est considéré comme une erreur opérationnelle (RFC 1912) qui peut entrainer le refus d'accès à un service. Par exemple, un serveur de messagerie électronique se présentant en envoi avec une adresse IP n'ayant pas de résolution inverse (PTR) a de grandes chances de se voir refuser, par l'hôte distant, la transmission du courrier (message de refus de type : IP lookup failed).

Une adresse IP peut être associée à plusieurs différents noms de domaine via l'enregistrement de plusieurs entrées PTR dans le sous-domaine .arpa dédié à cette adresse (in-addr.arpa. pour IPv4 et ip6.arpa. pour IPv6). L'utilisation d'enregistrements PTR multiples pour une même adresse IP est éventuellement présente dans le cadre de l'hébergement virtuel de multiples domaines web derrière la même adresse IP mais n'est pas recommandé dans la mesure où le nombre des champs PTR à renvoyer peut faire dépasser à la réponse la taille des paquets UDP de réponse et entraîner l'utilisation du protocole TCP (plus coûteux en ressources) pour envoyer la réponse à la requête DNS.

#### Les différents types d'enregistrements du DNS <a name="10"></a>

<u>Ressources web</u> :
- [Permet de visualiser toutes les infos DNS](http://dns-record-viewer.online-domain-tools.com/)
- [Tous les types d'enregistrements](https://www.google.com/search?q=dns+record+listing&oq=dns+record+list&aqs=chrome.2.69i57j0l5.5093j0j9&sourceid=chrome&ie=UTF-8)
- gandi.net > voir les fichiers de zone (totosandbox) : DNS, Types

![schema](https://docs.fedoraproject.org/en-US/Fedora/18/html/FreeIPA_Guide/images/dns-zone-record-list.png)

Les principaux enregistrements définis sont les suivants (via **nslookup**) :

**A record ou address record**

Cet enregistrement fait correspondre un nom d'hôte à une adresse IPv4 de 32 bits distribués sur quatre octets.

*Par exemple : hote.domaine.fr => 123.234.1.2*

**AAAA record ou IPv6 address record**

Cet enregistrement fait correspondre un nom d'hôte à une adresse IPv6 de 128 bits distribués sur seize octets.

*Par exemple : hote.domaine.fr => 2001:0db8:0000:85a3:0000:0000:ac1f:8001*

**CNAME record ou canonical name record**

Cet enregistrement permet de faire d'un domaine un alias vers un autre. Cet alias hérite de tous les sous-domaines de l'original.

Un enregistrement CNAME peut pointer vers un autre enregistrement CNAME mais cette méthode est déconseillée car elle double le nombre de requêtes au serveur DNS.

*Par exemple : www.domaine.fr => hote.domaine.fr*

**MX record ou mail exchange record**

Cet enregistrement défini les serveurs de courriel pour ce domaine. Un enregistrement MX ne peux pointer que vers un enregistrement A, et non un alias CNAME.

Par exemple si on défini le MX record de domain.fr comme étant l'adresse 123.234.1.3, les mails envoyés à @domaine.fr seront aiguillé vers cette même adresse.
PTR record ou pointer record

Cet enregistrement associe une adresse IP à un enregistrement de nom de domaine, aussi dit « reverse » puisque il fait exactement le contraire du A ou du AAA record. Il est indispensable à de nombreux services, qu'a chaque A ou AAA record corresponde sont PTR record.

*Par exemple : 123.234.1.2 => hote.domaine.fr*
> ```set type=mx``` (via *nslookup*)

**NS record ou name server record**

Cet enregistrement défini les serveurs DNS de ce domaine (les servers qui vont gérer la zone). Un enregistrement NS ne peux pointer que vers un enregistrement A, et non un alias CNAME.

Il peut y avoir plusieurs enregistrements NS si il existe plusieurs serveurs de messagerie sur le domaine.

*Par exemple, si on défini 123.234.1.1 comme NS record de domaine.fr, il sera alors un des serveurs consulté pour tout les sous domaine de .domain.fr comme par exemple hote.domaine.fr*

**SOA record ou Start Of Authority record**

Cet enregistrement donne les informations générales de la zone : serveur principal, courriel de contact, différentes durées dont celle d'expiration, numéro de série de la zone.

**Remarque:**

Il existe encore beaucoup d'autre type d'enregistrement (NAPTR, LOC, TXT, ).

Un enregistrement ne contient pas forcément une référence à une machine. par exemple un enregistrement TXT une chaîne de caractère (souvent utiliser pour précisé des paramètres de la zone DNS) ou encore l'enregistrement LOC qui peut contenir la localisation géographique d'une machine ou d'une zone DNS (latitude, longitude).


#### Quelques Considérations Opérationnelles sur le DNS <a name="11"></a>

- Protocole de base sous-jacent à tous les services
- Existance de server primaire et de server secondaire (mode slave)

**Mise à jour et cohérence du DNS**

Les mises à jour se font sur le serveur primaire du domaine, les serveurs secondaires recopiant les informations du serveur primaire dans un mécanisme appelé transfert de zone. Pour déterminer si un transfert de zone doit avoir lieu, le serveur secondaire consulte le numéro de version de la zone et le compare à la version qu'il possède. Le serveur primaire détermine à quelle fréquence le numéro de version est consulté. Quand un changement est effectué, les serveurs envoient des messages de notification aux serveurs secondaires pour accélérer le processus (transfert de zone entre deux servers ce sont de petits fichiers).

Il se peut que des informations qui ne sont plus à jour soient cependant conservées dans des serveurs cache. Il faut alors attendre l'expiration de leur *Time to live* pour que ces informations cachées disparaissent et donc que la mise à jour soit pleinement effective. On peut minimiser le temps nécessaire en diminuant le TTL associé aux noms de domaines qui vont être modifiées préalablement à une opération de changement.

Quand la liste des serveurs de noms change, ou quand une adresse IP est modifiée, le gestionnaire du domaine de niveau supérieur doit effectuer la mise à jour correspondante.

**Robustesse du DNS**

Pour éviter les points individuels de défaillance ([SPOF](https://fr.wikipedia.org/wiki/Point_de_d%C3%A9faillance_unique)), on évite de partager l'infrastructure entre les serveurs qui font autorité. Un serveur secondaire sera de préférence délocalisé et routé différemment que le serveur primaire.

Bien que cela soit techniquement possible, on évite de mêler sur un même serveur le rôle de DNS récursif et celui de serveur qui fait autorité.

De même, un hôte sera configuré avec plusieurs serveurs récursifs, de sorte que si le premier ne répond pas à la requête, le suivant sera employé. En général, les serveurs récursifs fournis par les FAI refusent les requêtes émanant d'adresses IP appartenant à d'autres FAI.

Il existe des services de DNS récursifs ouverts, c'est-à-dire qu'ils acceptent les requêtes de tous les clients. Il est donc possible à un utilisateur de configurer ceux-ci en lieu et place de ceux fournis par le FAI. Ceci pose cependant les problèmes suivants :

1. il n'y a pas de garantie que les réponses fournies seront les mêmes qu'avec des serveurs récursifs habituels. Un tel service pourrait en effet faire référence à une autre hiérarchie depuis la racine, disposer de TLD additionnels non standard, restreindre l'accès à certains domaines, voire altérer certains records avant leur transmission au client.

2. il n'y a pas de garantie de confidentialité, c'est-à-dire que ce service pourrait déterminer à quels domaines un utilisateur à accès en conservant des traces des requêtes DNS.

### **Sécurité du DNS** <a name="12"></a>


Le protocole DNS a été conçu avec un souci minimum de la sécurité. Plusieurs failles de sécurité du protocole DNS ont été identifiées depuis. Les principales failles du DNS ont été décrites dans le [RFC 3833](https://datatracker.ietf.org/doc/html/rfc3833) publié en août 2004. 

En voici quelques exemples :

#### **Interception des paquets**

Une des failles mises en avant est la possibilité d'intercepter les paquets transmis. Les serveurs DNS communiquent au moyen de paquets uniques et non signés. Ces deux spécificités rendent l'interception très aisée. L'interception peut se concrétiser de différentes manières, notamment via une attaque de type « man in the middle », de l'écoute des données transférées et de l'envoi de réponse falsifiée (voir paragraphe ci-dessous).

<u>Ressources web</u> :
- [Ionos](https://www.ionos.fr/digitalguide/serveur/securite/quest-ce-que-le-dns-hijacking/)

#### **Fabrication d'une réponse**

Les paquets des serveurs DNS étant faiblement sécurisés, authentifiés par un numéro de requête, il est possible de fabriquer de faux paquets. Par exemple, un utilisateur qui souhaite accéder au site http://mabanque.example.com fait une demande au site DNS. Il suffit à ce qu'un pirate informatique réponde à la requête de l'utilisateur avant le serveur DNS pour que l'utilisateur se retrouve sur un site de phishing.

#### **Corruption des données**

La trahison par un serveur, ou corruption de données, est, techniquement, identique à une interception des paquets. La seule différence venant du fait que l'utilisateur envoie volontairement sa requête au serveur. Cette situation peut arriver lorsque, par exemple, l'opérateur du serveur DNS souhaite mettre en avant un partenaire commercial.

#### **Empoisonnement du cache DNS**

![schema](https://www.imperva.com/learn/wp-content/uploads/sites/13/2019/01/DNS-spoofing.jpg)

L'empoisonnement du cache DNS ou pollution de cache DNS (DNS cache poisoning ou DNS cache pollution en anglais) est une technique permettant de leurrer les serveurs DNS afin de leur faire croire qu'ils reçoivent une requête valide tandis qu'elle est frauduleuse. Une fois que le serveur DNS a été empoisonné, l'information est mise dans un cache, rendant ainsi vulnérable tous les utilisateurs de ce serveur. Ce type d'attaque permet, par exemple, d'envoyer un utilisateur vers un faux site dont le contenu peut servir à de l'hameçonnage (dans le cas du DNS, on parle de pharming) ou comme vecteur de virus et autres applications malveillantes.

Un ordinateur présent sur Internet utilise normalement un serveur DNS géré par le fournisseur d'accès. Ce serveur DNS est la plupart du temps limité aux seuls utilisateurs du réseau du fournisseur d'accès et son cache contient une partie des informations rapatriées par le passé. Une attaque par empoisonnement sur un seul serveur DNS du fournisseur d'accès peut affecter l'ensemble de ses utilisateurs, soit directement ou indirectement si des serveurs esclaves s'occupent de propager l'information.

<u>Ressources Web :</u>
- [DNS poisoning par Okta](https://www.okta.com/identity-101/dns-poisoning/)
- [Page wikipedia](https://fr.wikipedia.org/wiki/Empoisonnement_du_cache_DNS)

#### **Déni de Service : DDOS**

![schema](https://exploitszone.com/wp-content/uploads/2020/06/ddos-attack.png)

Une attaque par déni de service (ou attaque par saturation ; en anglais, Denial of Service attack ou DoS attack) est une attaque sur un serveur informatique consistant envoyer une grande quantité de requête à celui-ci pour le saturer. Une fois saturé il ne peut plus fournir de service aux clients réguliers..

<u>Ressources Web</u> :
- [Page Wikipedia](https://fr.wikipedia.org/wiki/Attaque_par_d%C3%A9ni_de_service)
- [Securiteinfo](https://www.securiteinfo.com/attaques/hacking/ddos.shtml)
- [Cisco](https://www.cisco.com/c/fr_fr/products/security/what-is-a-ddos-attack.html)
- [Zdnet](https://www.zdnet.fr/pratique/qu-est-ce-qu-une-attaque-ddos-tout-savoir-pour-les-reconna-tre-et-s-en-proteger-39911475.htm)
- [Ionos](https://www.ionos.fr/digitalguide/serveur/know-how/quest-ce-que-le-dos-denial-of-service/)

#### **Fondamental : DNSSEC**

![schema](https://www.efficientip.com/wp-content/uploads/2020/01/chain-of-trust-part1.svg)

- DNSSEC permet de sécuriser les données envoyées par le DNS. Contrairement à d'autres protocoles comme SSL, il ne sécurise pas juste un canal de communication mais il protège les données, les enregistrements DNS, de bout en bout. Ainsi, il est efficace même lorsqu'un serveur intermédiaire trahit.

- DNSSEC signe cryptographiquement les enregistrements DNS et met cette signature dans le DNS. Ainsi, un client DNS méfiant peut récupérer la signature et, s'il possède la clé du serveur, vérifier que les données sont correctes. La clé peut être récupérée via le DNS lui-même (ce qui pose un problème d'œuf et de poule) ou bien par un autre moyen (diffusée via le Web et signée avec PGP par exemple).

- DNSSEC permet de déléguer des signatures : ainsi, le registre d'un domaine de premier niveau peut annoncer que tel sous-domaine est signé. On peut ainsi bâtir une chaîne de confiance depuis la racine du DNS.

- DNSSEC introduit aussi ses propres problèmes, par exemple, le fait qu'un enregistrement spécial (NSEC) indique le prochain domaine de la zone permet d'énumérer le contenu complet d'une zone signée, même si le transfert de zone n'est pas permis. Ce problème fait que la plupart des TLD utilisent l'enregistrement NSEC3, qui n'a pas ce défaut.

<u>Ressources Web</u> :
- [ICANN](https://www.icann.org/resources/pages/dnssec-what-is-it-why-important-2019-03-20-fr)

### **DNS par Stéphane Bortzmeyer** <a name="13"></a>

- Server DNS le plus répendu : [BIND](https://fr.wikipedia.org/wiki/BIND) (peut faire server faisant autorité *OU* résolveur)
- Autre logiciel DNS pour server faisant autorité : [NSD](https://fr.wikipedia.org/wiki/Name_Server_Daemon) (plus rapide que Bind, nombre de codes 20 fois plus petit, une seule faille historique)
- Emacs (éditeur de fichier comme nano sur Linux)
- Le server résolver interroge par hasard les servers faisant autorité (Bind), et utilise le plus rapide (même s'il lui arrive de changer pour éviter le poisonning)

#### **Le protocole en Video par S.Bortzmeyer** 

Stéphane Bortzmeyer est informaticien à l’Association française pour le nommage Internet en coopération (Afnic). Il s'occupe entre autres de sécurité, notamment du DNS. Il est membre de Gitoyen[réf. nécessaire] et du conseil d'administration du France-IX, le principal point d'échange Internet français. Membre actif de l'IETF, il est l'auteur de plusieurs RFC, notamment liés aux questions de DNS et de vie privée. 

||**Cours magitral**|**Questions techniques**|
|:-:|:-:|:-:|
|**Conférence**|[![Cours magitral](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/DNS_stephane.jpg)](https://www.youtube.com/watch?v=QHVK666TFUI)|[![Partie Technique](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/bind.jpg)](https://www.youtube.com/watch?v=KFHZL6bxsUo)|

**DNS** <br/>
= infrastructure<br/>
= base de données décentralisée<br/>
= associe données à noms de domaine (noms uniques/mémorisables/vecteur identité/arborescent) + résoudre noms en données<br/>
= rien sur l'internet ne marche sans le DNS <br/>

**Deux types de server DNS** :
- *Server faisant autorité* = server dns qui connait le contenu d'un domaine (server afnic qui connaissent ce qu'il y a dans .fr)
- *Résolveur ou server récusif* = server dns qui ne connait rien mais pose des questions aux servers faisant autorité et mémorise les réponses (FAI, Réseau local)

**Risques**
- Risque lié à l'enregistrement (détournement, saisie, justice...)
- Risque technique de panne (**résilience** : continuer à fonctionner ; ex. il existe une 150aine de servers physiques pour le .fr)
- Risque par attaque par empoisonnement (déploiement DNSSEC)<br/>
-> il s'agit de répondre avant le vrai server auprès du résolveur qui va mémoriser la réponse<br/>
-> utiliser le chiffrement par clef/signature pour empêcher l'empoisonnement

**Organisations et pouvoirs : les processus mous et les différents acteurs**

- Gouvernement des USA (possède la racine)
- ICANN (gère la racine pour le gouvernement des USA)
- Registres de TLD (Verisign, AFNIC...) et BE
- Opérateurs de résolveurs (résolveurs menteurs de certains FAI qui bloquent certains contenus...)
- Auteurs de logiciels (permission DNSSEC ou pas...)

**Alternatives**

- identificateurs fondés sur le contenu comme magnets (châine de caractères qui donne les infos sur le contenu, l'endroit... = privilégie le contenu et non le server) de BitTorrent
- identificateurs fondés sur la cryptographie comme ceux de BitMessage (les adresses sont des clefs crypotagraphiques = suite de chiffres)

#### Ressources web

- [Son blog](https://www.bortzmeyer.org/)
- [Article : dns-over-https](https://www.nextinpact.com/article/30142/108783-dns-over-https-pour-stephane-bortzmeyer-diable-est-dans-details)

|**Sécurité DNS**|
|:-:|
[![Cours magitral](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/S%C3%A9cu_bors.jpg)](https://www.youtube.com/watch?v=wg45iVWuEKE)

---

---

### **Exercices** <a name="14"></a>

- [Questionnaire](https://docs.google.com/document/d/1ZSy_dOYGScy3gDfcS09Zbo3ArixWlrfoNBL3iTwZEBM/edit)

> ```ipconfig/displaydns>rapport.txt``` (pour récupérer les infos dans un fichier texte)

#### **Les 30 questions à répondre**


1. **Créer et remplir un tableau de 14 lignes et de 6 colonnes (Lettre Root, Nom entité, description entité, IPv4, IPv6, nb d'instance) . Ce tableau sera très utile pour window server et Bind9**

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/infos_server_racines.jpg)

2. **Capturer une requête DNS dans Wireshark entre votre client et un serveur OPENDNS, montrer dans la capture la réponse du serveur UDP à votre requête sur www.republiquedesmangues.fr**

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/rep_mangues_wireshark.jpg)

3. **Capturer une requête DNS dans Wireshark en TCP**

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/dns_tcp.jpg)

- [Using TCP with Lookup](https://www.sourcedaddy.com/windows-7/using-tcp-for-dns-lookups.html#:~:text=Using%20TCP%20for%20DNS%20Lookups%20When%20a%20DNS,deliver%20all%20the%20DNS%20records%20in%20the%20response)


4. **Vider votre cache et Capturer votre cache DNS dans un fichier Texte, le traffic Google pour faire une recherche Linkedin, vous identifier dedans et isoler dans ce fichier seulement les FQDN.**

- ipconfig/flushdns
- [ipconfig/displaydns>cache.txt](https://cefimeu-my.sharepoint.com/:t:/g/personal/rdelmas_cefim_eu/Ed5mDROc5OxHrhfgJzFlk0cBSImrthZOw5MAzM6V_Sesgg?e=cRQkBb)
- Google / Linkedin / Connexion
- [ipconfig/displaydns>cache2.txt](https://cefimeu-my.sharepoint.com/:t:/g/personal/rdelmas_cefim_eu/EeVBwxPybylAggiUMfitfaQB-yB7P_fEewaES2viN_c8BA?e=ZtXci2)
- FQDN = nom de domaine qui donne la position exacte de son nœud dans l'arborescence DNS
- [ipconfig/displaydns>cache3.txt](https://cefimeu-my.sharepoint.com/:t:/g/personal/rdelmas_cefim_eu/EeVBwxPybylAggiUMfitfaQB-yB7P_fEewaES2viN_c8BA?e=ZtXci2)


5. **Faire un DIG (donc sur Linux) simple en A sur le nom de domaine du site https://hooooooooo.com/**

- [Ressource Web](https://www.hostinger.fr/tutoriels/comment-utiliser-la-commande-dig-sous-linux)
- ``` dig hooooooooo.com/ +short```

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/digA.jpg)
![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/dig_short.jpg)

6. **Faire un DIG plus complet sur Elysee.fr**

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/dig_noall.jpg)

7. **Quel est le nom FQDN du cluster d'hébergement de objectif2038.net?**

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/nslookup_reverse.jpg)

8. **Quel est le CNAME de www.objectif2038.net ?**

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/cname.jpg)

9. **Quel est le nom du serveur prioritaire MX pour le domaine ID37.fr (Dans un MX le serveur prioritaire est il 1 ou 99?)**

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/server_mx.jpg)

- Il s'agt du n°1

10. **Quelle est la clé MS dans le record TXT pour le passage à Office365 du domaine cefim.ninja ?**

- [Ressource Web](https://docs.microsoft.com/fr-fr/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider?view=o365-worldwide)

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/clef_mx.jpg)

11. **Quel est l'email de contact pour le domaine cant-not-tweet-this.com ?**

- mode TXT
- *hostmaster@nsone.net*

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/mail_txt.jpg)

12. **Quelles sont les coordonnées LAT,LON de l'instance root-servers la plus septentrionale?**

- https://root-servers.org/
- Nuuk, Groenland, Latitude : 64.175029 | Longitude : -51.735539

- nslookup
- set mode=loc
- IPv4 : 193.0.14.129

13. **Trouver un record TXT "fun" via une recherche genre https://medium.com/@fabianbeiner/fun-with-txt-records-3752fa5680a4**

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/txt_fun.jpg)

14. **Combien coûte l'enregistrement de tinytuba.tours sur Gandi ?**

- Via le site, recherche du nom de domain
- Coût annuel 59,60 euros

15. **Quand le domaine thatsthefinger.com sera t'il disponible ?**

- http://www.whois-raynette.fr/
- Registrar Registration Expiration Date: 2021-11-16T07:53:48Z

16. **Chez quel hébergeur est le site de la mairie de Montcuq ?**

- La mairie utilise OVH

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/montcul.jpg)

17. **Capturer un geotrace IP pour le domaine fallingfalling.com**

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/tracert.jpg)

18. **Lister les IP et les FQDN des routeurs rencontrés entre vous et Amazon japon**

- tracert amazon.co.jp

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/amazon_jp.jpg)

19. **Trouver la liste des Servers DNS publics en Antarctique**

- https://public-dns.info/
- https://public-dns.info/nameserver/aq.html

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/amazon_jp_hop.jpg)

20. **Quel est la législation du TLD pour Macao?**

- [Page wikipedia TLD_pays](https://en.wikipedia.org/wiki/Country_code_top-level_domain#Lists)
- extension : *.mo*
- Les titulaires doivent avoir une entreprise enregistrée à Macao, avec le même nom que le domaine qu'ils souhaitent enregistrer. 

21. **Combien y a t-il de sites en Corée du nord?**

- [Page wikipedia .kp](https://en.wikipedia.org/wiki/.kp)
- A moins 9 domaines de premier niveau .kp et plus de 30 domaines sont accessibles sur l'Internet mondial

22. **Synthétiser en 10 lignes la story de sex.com**

En mai 1994, Gary Kremen a enregistré *sex.com* auprès de Network Solutions, sans le développer. L'année suivante, ladite société a transféré, sans autorisation, le domaine à Stephen M. Cohen, celui-ci ayant soumis un faux fax pour arriver à cette fin. Dans la foulée, Cohen a utilisé l'allocation évocation du nom de domaine/publicité pour engranger beaucoup d'argent. S'en est suivi une bataille juridique entre Cohen et Kremen sur fond de l'infrastructure d'enregistrement des noms de domaine. Kremen a remporté la victoire en novembre 2000, lorsqu'il a été ordonné à Network Solutions de rendre le domaine au plaignant et à Cohen un remboursement de plusieurs dizaines de millions d'euros. 

23. **Quel est le BE pour potamochère.fr**

- WHOIS
- [Site de l'AFNIC pour trouver le BE](https://www.afnic.fr/noms-de-domaine/tout-savoir/annuaire-bureaux-enregistrement/)
- Bureau d'enregistrement : GANDI

24. **Combien y a t il de nom de domaines .fr enregistrés ?**

- [Rapport AFNIC](https://www.afnic.fr/observatoire-ressources/actualites/rapport-annuel-2020-transition-numerique-lafnic-et-le-fr-aux-cotes-des-tpe-pme/)
- 31/12/2020 : 3 670 372 noms de domaine
- Source : [Velhost](https://velhost.fr/web/combien-de-noms-de-domaine-en-fr-sont-enregistres-chaque-mois/) pour un graphique montrant la répartition des noms de domaine

25. **Obtenir la liste des Registrars pour l'AFNIC**

- [Liste des bureaux d'enregistrements](https://www.afnic.fr/noms-de-domaine/tout-savoir/annuaire-bureaux-enregistrement/)

26. **Qui est le CEO fondateur gerant le TLD .sexy?**
- Société [Uniregistry](https://en.wikipedia.org/wiki/Uniregistry)
- CEO : Frank Schilling

27. **Quel est le pourcentage de  volume des Requêtes TCP(V4 et V6) par rapport aux UDP pour le premier server racine de Verisign le 25 décembre 2018 ?**

- https://root-servers.org/
- A, Verisign
- Statistics
- [Archives 2018](https://a.root-servers.org/raw-data/index.html)
- [Volume Traffic 25/12/2018](https://a.root-servers.org/raw-data/index.html)

UDP = 4374249647 (ipv4) + 743326738 (ipv6) = 5 117 576 385
TCP = 126256701 (ipv4) + 33257206 (ipv6) = 159 513 907

- 25/12/2018 : 5 277 090 292 requêtes, dont 97% en UDP et 3% en TCP

28. **Quel est le numéro de série du serveur qui gère eelslap.com ?**

- http://www.whois-raynette.fr/whois/eelslap.com
- ns1.mediatemple.net

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/id_server.jpg)

- Serial number server : 2020070101

29. **A qui appartient la plage d'IP du domaine endless.horse?**

- [Page Wikipedia TLD](https://en.wikipedia.org/wiki/List_of_Internet_top-level_domains#H)
- Société : [Minds + Machines](https://mmx.co/)

30.     Tester et faire des captures d'utilisation des soft de cet article : https://www.cnetfrance.fr/news/trois-logiciels-pour-optimiser-les-dns-vos-mises-a-jour-hebdo-39785896.htm

**DNS Jumper**

- [Lien de téléchargement](https://www.cnetfrance.fr/telecharger/dns-jumper-39958521s.htm)

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/DNS_jmper_test.jpg)

**NameBench**

- [Lien de téléchargement](https://www.cnetfrance.fr/telecharger/namehelp-40337377s.htm)

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/namebench4.png)

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/namebench1.png)

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/namebench2.png)

![*](https://raw.githubusercontent.com/RaspCric/In-girum-imus-nocte-et-consumimur-igni/images/namebench3.png)


**NameHelp**

- [Lien de téléchargement](https://fr.freedownloadmanager.org/Windows-PC/Namehelp-GRATUIT.html)
- http://localhost:53533/#dashboard