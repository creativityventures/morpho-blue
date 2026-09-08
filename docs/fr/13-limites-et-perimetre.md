# Chapitre 13 — Limites connues et perimetre de ce parcours

Morpho Blue est volontairement un protocole de base minimal : il ne fournit lui-meme ni interface de gestion de risque, ni selection de marches recommandes, ni repartition automatique de la liquidite. Ces couches existent dans l'ecosysteme Morpho sous forme de coffres tiers (dont MetaMorpho, un contrat ERC-4626 qui repartit les depots des utilisateurs entre plusieurs marches Morpho Blue selon une strategie de risque choisie par un gestionnaire de coffre) : ce depot ne les contient pas et ils sont hors perimetre de ce parcours.

Ce parcours ne couvre pas en detail `MathLib.sol` (les fonctions `mulDiv`/`wTaylorCompounded` elles-memes), `UtilsLib.sol`, `SafeTransferLib.sol`, ni les mocks du dossier `src/mocks/` fournis pour les tests. Le contrat `IOracle` n'est qu'une interface : Morpho Blue ne fournit ni n'audite lui-meme aucune implementation d'oracle de prix, une responsabilite entierement deleguee au createur de chaque marche.

Rien n'a ete installe, compile, deploye ni execute pour ecrire ces chapitres. Aucun test n'a ete lance ; ces chapitres decrivent ce que le code Solidity dit faire, en renvoyant aux fichiers cites. Le depot fournit sa propre suite de tests (dossier `test/`, hors du clone superficiel utilise ici) pour verification independante.
