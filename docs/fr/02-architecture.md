# Chapitre 2 — Architecture en singleton : des marches identifies par hash

Morpho Blue est un singleton : un seul contrat `Morpho` heberge tous les marches, plutot qu'un contrat de marche par paire d'actifs. Un marche est decrit par la structure `MarketParams` (`loanToken`, `collateralToken`, `oracle`, `irm`, `lltv`) ; `MarketParamsLib.id` calcule son identifiant, un `Id` de type `bytes32`, en hachant directement les 160 octets memoire de cette structure par `keccak256` en assembleur — une methode nettement plus econome en gaz qu'un `abi.encode` classique.

`createMarket` verifie seulement que le modele de taux (`isIrmEnabled`) et le seuil de liquidation (`isLltvEnabled`) ont ete pre-approuves par le proprietaire du protocole (chapitre 12), puis enregistre le marche : aucune approbation specifique a la paire d'actifs ou a l'oracle choisi n'est necessaire. N'importe qui peut ainsi lancer un marche avec un oracle de son choix, y compris malveillant — la securite d'un marche donne devient alors la responsabilite de qui y interagit, pas du protocole.

Le mapping `market[id]` stocke l'etat mutable du marche (soldes totaux, indices temporels), `idToMarketParams[id]` conserve les parametres d'origine pour verification, et `position[id][compte]` stocke la position de chaque utilisateur sur ce marche precis. Le protocole ne connait donc aucune paire d'actifs a l'avance : tout est parametre au moment de la creation du marche.

[Chapitre suivant : comptabilite par parts (shares)](03-parts.md)
