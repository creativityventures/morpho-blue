# Chapitre 6 — borrow, repay et le controle de sante (LLTV)

`borrow` incremente les parts et le montant emprunte du compte cible, puis exige deux conditions avant de transferer les fonds : `_isHealthy` (la position reste suffisamment collateralisee) et `totalBorrowAssets <= totalSupplyAssets` (le marche a effectivement la liquidite disponible). `_isHealthy` compare la dette actuelle du compte (`borrowShares` convertis en actifs, arrondis vers le haut au detriment de l'emprunteur) a sa capacite maximale d'emprunt, calculee comme la valeur de son collateral au prix de l'oracle, multipliee par le LLTV (loan-to-value liquidation) du marche.

Le prix retourne par l'oracle est interprete a une echelle fixe, `ORACLE_PRICE_SCALE` = 1e36, quel que soit le nombre de decimales des deux jetons du marche : c'est a l'oracle fourni au marche de normaliser correctement son prix a cette echelle, le contrat `Morpho` lui-meme ne connait ni ne verifie les decimales des jetons.

`repay` est le miroir exact de `borrow` : reduction des parts et du montant emprunte, avec la meme regle d'arrondi inversee (rembourser un montant d'actifs brule les parts vers le bas, au benefice de l'emprunteur cette fois), suivi d'un `safeTransferFrom` qui preleve le remboursement — avec, comme pour `supply`, un callback optionnel `onMorphoRepay` avant le transfert.

[Chapitre suivant : supplyCollateral et withdrawCollateral](07-collateral.md)
