#  Exercice 11 :  DNS 

### Informations
- Évaluation : formative.
- Durée estimée : 2 heures.
- Système d'exploitation : Ubuntu client ou Windows.
- Environnement : Docker.  

### Objectifs  

- Comprendre le DNS.
- Comprendre le principe de DNS à l’intérieur dans Docker.

Dans cet exercice, vous allez constater à quel point il peut être fastidieux de trouver une résolution d’adresse sans un serveur récursif. Heureusement nous allons disposer d'un bon serveur DNS récursif, qui fait tout ce travail à notre place.

Un DNS récursif garde en mémoire ce qu'il trouve en effectuant cette recherche et s'en resservira pour d'éventuelles résolutions futures. Les serveurs « qui font autorité » indiquent une durée de validité pour les informations qu'ils donnent. Ainsi, les serveurs récursifs devront rafraichir le contenu de leur cache en fonction de dette durée de validité.

Vous allez également comprendre comment les conteneurs se « trouvent » dans Docker et comprendre que le DNS est la clé pour faciliter les communications entre conteneurs. Vous allez aussi découvrir comment ça fonctionne par défaut avec les réseaux personnalisés.

Vous avez vu que les conteneurs se retrouvent dans un réseau virtuel privé dans Docker et chacun des conteneurs se voient attribuer une adresse IP. Par contre, les conteneurs ne doivent pas compter sur les adresses IP pour l'intercommunication, car ces adresses peuvent changer. Docker possède un DNS intégré qui utilise les noms des conteneurs (il est également possible de créer des alias) comme enregistrement. Il est donc possible d’utiliser ce DNS dans vos réseaux personnalisés (le réseau « bridge » n’a pas de DNS).


## Section 1 : DNS et récursivité

### Étape 1 : sous Windows

Utiliserz un poste Windows, soit votre propre ordinateur ou une VM, et répondez aux questions.

- Qu'elle est le serveur de nom (DNS) pour votre poste client ?
	<details>
	<summary>Réponse</summary>
	Varie.
	</detail>

- Quelle commande avez-vous utilisée ? 
	<details>
	<summary>Réponse</summary>
	`nslookup`
	</detail>

- Faites un nslookup sur le nom de domaine : csfoy.ca

	Qui vous a répondu ? Est-ce que la réponse fait autorité ?
	<details>
	<summary>Réponse</summary>
	Votre serveur DNS.
	Si vous êtes à l'intérieur du cégep, oui. Sinon, non.
	</detail>

- Faites un nslookup sur le nom de domaine : gouv.qc.ca

	Qui vous a répondu ? Est-ce que la réponse fait autorité ? 
	<details>
	<summary>Réponse</summary>
	Votre serveur DNS.
	Non, elle n'est pas autoritée.
	</detail>

- Essayer à nouveau avec un nslookup sur le nom de domaine : www.google.com

	Qui vous as répondu ? Est-ce que la réponse fait autorité ?
	<details>
	<summary>Réponse</summary>
	Votre serveur DNS.
	Non, elle n'est pas autoritée.
	</detail>

- À partir des expérience précédente, a quel moment la réponse fait autorité ? 
	<details>
	<summary>Réponse</summary>
	La réponse fait autorité lorsque le serveur DNS qui nous répond est celui du FQDN.
	</detail>


### Étape 2 : sous Linux


