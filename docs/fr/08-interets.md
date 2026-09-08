# Chapitre 8 — accrueInterest : un modele de taux externe et pluggable

Morpho Blue ne code aucun modele de taux d'interet en dur : chaque marche reference un contrat `irm` externe, pre-approuve par le proprietaire (chapitre 12) mais choisi librement par le createur du marche. `_accrueInterest` interroge ce contrat via `IIrm(marketParams.irm).borrowRate(marketParams, market[id])` pour obtenir un taux, puis capitalise l'interet sur `totalBorrowAssets` et `totalSupplyAssets` en une seule fois avec `wTaylorCompounded`, une approximation de Taylor de la composition exponentielle adaptee au temps ecoule depuis la derniere mise a jour (`market[id].lastUpdate`).

Si le marche facture des frais (`market[id].fee`, plafonne a 25 % par `MAX_FEE` dans `ConstantsLib`), une partie de l'interet nouvellement cree est convertie en parts de preteur supplementaires, attribuees non pas aux preteurs existants mais au `feeRecipient` designe par le proprietaire du protocole — un mecanisme de frais entierement optionnel, actif uniquement sur les marches ou la gouvernance a explicitement fixe un taux non nul via `setFee`.

Cette externalisation totale du modele de taux (contrairement au modele a double pente fige d'Aave, Compound v2/v3 ou MakerDAO deja documentes pour ce compte ou pour d'autres) permet a n'importe quel createur de marche de brancher sa propre courbe de taux, du moment que le contrat IRM utilise a ete pre-valide par la gouvernance du protocole comme sur.

[Chapitre suivant : liquidate et la bad debt socialisee](09-liquidation.md)
