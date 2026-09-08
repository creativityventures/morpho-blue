# Chapitre 4 — SharesMathLib : des parts virtuelles contre l attaque par inflation

Un marche fraichement cree n'a ni parts ni actifs : le tout premier deposant pourrait, sur un vault ERC-4626 naif, deposer un montant infime pour recevoir une part, puis transferer directement des actifs au contrat pour gonfler artificiellement le ratio actifs/parts et voler la valeur des deposants suivants par arrondi. C'est l'attaque par inflation documentee par OpenZeppelin pour les vaults ERC-4626, et `SharesMathLib` s'en protege par la meme methode : des **parts virtuelles**.

`VIRTUAL_SHARES` (fixe a 1 000 000) et `VIRTUAL_ASSETS` (fixe a 1) sont ajoutes de part et d'autre de chaque conversion (`toSharesDown`, `toAssetsDown`, `toSharesUp`, `toAssetsUp`) : le marche se comporte partout comme s'il possedait deja un million de parts virtuelles pour un actif virtuel, meme quand ses totaux reels sont a zero. Un attaquant qui tenterait de gonfler le ratio devrait alors deplacer des sommes disproportionnees par rapport au gain possible, ce qui rend l'attaque non rentable sans qu'aucune part minimale forcee ni verrouillage initial ne soit necessaire.

Le commentaire du code souligne un corollaire important : ces parts virtuelles ne pourront jamais etre racheteees contre de vrais actifs — elles se comportent comme une dette theorique permanente et non realisable, un artefact mathematique du modele plutot qu'un veritable passif du protocole.

[Chapitre suivant : supply et withdraw du jeton emprunte](05-supply-withdraw.md)
