# Chapitre 3 — La comptabilite par parts (shares) plutot que par montant

Comme un vault ERC-4626, Morpho Blue ne stocke jamais directement un solde en actif pour un utilisateur : il stocke un nombre de **parts** (`supplyShares` pour les preteurs, `borrowShares` pour les emprunteurs), converties en montant reel via le ratio courant entre parts totales et actifs totaux du marche (`totalSupplyShares`/`totalSupplyAssets`, `totalBorrowShares`/`totalBorrowAssets`). Quand l'interet s'accumule (chapitre 8), seuls les actifs totaux augmentent : chaque part existante vaut alors mecaniquement un peu plus, sans qu'aucune boucle de mise a jour par compte ne soit necessaire.

`supply`/`withdraw`/`borrow`/`repay` acceptent chacun soit un montant d'actifs, soit un nombre de parts, jamais les deux a la fois (`UtilsLib.exactlyOneZero`) : l'appelant choisit quelle grandeur il veut fixer precisement, l'autre etant calculee par conversion. Fournir un montant d'actifs a `supply` arrondit les parts obtenues vers le bas (au benefice du protocole), tandis que retirer un montant d'actifs via `withdraw` arrondit les parts brulees vers le haut — un arrondi systematiquement defavorable a l'utilisateur et favorable a la solvabilite globale du marche.

Cette double API (par actifs ou par parts) est reprise a l'identique pour l'emprunt : `borrow` avec un montant d'actifs arrondit les parts empruntees vers le haut (l'emprunteur doit legerement plus), preservant la meme logique de marge de securite au benefice du protocole a chaque conversion.

[Chapitre suivant : les parts virtuelles contre la manipulation de prix](04-parts-virtuelles.md)
