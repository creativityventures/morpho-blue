# Chapitre 7 — supplyCollateral et withdrawCollateral : un solde sans parts

Contrairement au jeton emprunte, le collateral ne beneficie d'aucune comptabilite par parts : `position[id][onBehalf].collateral` est un montant brut, incremente ou decremente directement par `supplyCollateral`/`withdrawCollateral`, sans jamais rapporter d'interet ni etre mutualise avec les autres deposants de collateral. Ce choix simplifie le modele : le collateral d'un compte n'appartient qu'a ce compte, il n'existe pas de pool de collateral partage dans lequel les parts de chacun fluctueraient.

`supplyCollateral` ne verifie meme pas la sante de la position apres le depot (ajouter du collateral ne peut jamais rendre un compte moins sain), tandis que `withdrawCollateral` exige `_isHealthy` apres le retrait, exactement comme `borrow` exige la sante apres l'emprunt — les deux operations qui peuvent degrader la solvabilite d'un compte partagent la meme verification finale.

`supplyCollateral` accepte elle aussi un callback optionnel (`onMorphoSupplyCollateral`), utile par exemple pour swapper un actif en collateral juste avant de le deposer dans la meme transaction, un motif courant dans les strategies de levier en un seul appel.

[Chapitre suivant : accrueInterest, l IRM externe et les frais](08-interets.md)
