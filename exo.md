Convention: J'utilise la syntaxe suivante pour signifier une variable: [variable]

# Exo 1
https://spoonless.github.io/epsi-i4-web-services/http/http_cas_utilisation.html

Vous devez utiliser l’API Web du site
http://rest-bookmarks.herokuapp.com pour réaliser les opérations
suivantes :

- Créer une nouvelle ressource bookmark (montrez qu’il est possible d’utiliser deux méthodes HTTP différentes)

	curl -v --data-binary "name=dtabarie&description=value&url=value" https://rest-bookmarks.herokuapp.com/api/bookmarks

- Obtenir la représentation de la ressource bookmark que vous avez créée

	curl -v -X GET https://rest-bookmarks.herokuapp.com/api/bookmarks/latest

- Mettre à jour la ressource bookmark que vous avez créée

	curl -v -X PUT --data-binary "name=newname&url=newurl&description=newdesc" https://rest-bookmarks.herokuapp.com/api/bookmarks/dtabarie

- Supprimer la ressource bookmark que vous avez créée

	curl -v -X DELETE https://rest-bookmarks.herokuapp.com/api/bookmarks/dtabarie

	vérif

	curl -v -X GET https://rest-bookmarks.herokuapp.com/api/bookmarks/dtabarie
	(le serveur doit donc renvoyer une erreur 404)

- Mettre à jour la dernière ressource bookmark ajoutée par n’importe quel client

	Dans ce cas il est nécessaire de faire, un get sur latest pour connaître le nom du dernier utilisateur.
	Nous pouvons ensuite utiliser cette information dans un PUT:

	curl -v -X PUT --data-binary "name=newname&url=newurl&description=newdesc" https://rest-bookmarks.herokuapp.com/api/bookmarks/[lastname]

# Exo 2
Utilisez l’API Web du site http://rest-bookmarks.herokuapp.com pour
expérimenter la négociation de contenu proactive. À partir d’un
bookmark que vous aurez créé avec cette API, essayez de réaliser une
négociation de contenu sur le type de représentation (avec l’en-tête
Accept). Trouvez des cas pour lesquels :

- vous obtenez un format de représentation différent de celui par défaut

    curl -v GET -H 'Accept: application/xml' http://rest-bookmarks.herokuapp.com/api/bookmarks/

- vous obtenez une réponse 406 de la part du serveur

    curl -v GET -H 'Accept: text/html' http://rest-bookmarks.herokuapp.com/api/bookmarks/

# Exo 3
Vous devez utiliser l’API Web du site
http://rest-bookmarks.herokuapp.com pour expérimenter les requêtes
conditionnelles. À partir d’un bookmark que vous aurez créé avec cette
API, vous devez utiliser les requêtes conditionnelles pour :

- demander une représentation d’un bookmark que si ce dernier a été mis à jour

    curl -v -X GET -H "If-Modified-Since:[Day], [DayNb] [Month] [Year] [hours:minutes:seconds] GMT" http://rest-bookmarks.herokuapp.com/api/bookmarks/[bookmarkNb]

- empêcher de créer un bookmark s’il existe déjà un bookmark avec la même URI



- signaler une erreur pour la suppression d’un bookmark qui n’existe pas

	curl -v -H "0000000" http://rest-bookmarks.herokuapp.com/api/bookmarks/[bookmarkNb]
