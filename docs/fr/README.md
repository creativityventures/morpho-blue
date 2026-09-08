# Parcours francais de Morpho Blue — Pret et emprunt

Lecture commentee du protocole de marches de pret isoles Morpho Blue, en francais, un mecanisme par chapitre.
Aucun code n'a ete installe, compile ni execute : ce parcours est purement documentaire.

1. [Presentation de Morpho Blue](01-presentation.md)
2. [Architecture en singleton : des marches identifies par hash](02-architecture.md)
3. [La comptabilite par parts (shares) plutot que par montant](03-parts.md)
4. [SharesMathLib : des parts virtuelles contre l attaque par inflation](04-parts-virtuelles.md)
5. [supply et withdraw : le cote preteur du marche](05-supply-withdraw.md)
6. [borrow, repay et le controle de sante (LLTV)](06-borrow-repay.md)
7. [supplyCollateral et withdrawCollateral : un solde sans parts](07-collateral.md)
8. [accrueInterest : un modele de taux externe et pluggable](08-interets.md)
9. [liquidate : un facteur d incitation derive du LLTV et la bad debt socialisee](09-liquidation.md)
10. [flashLoan et les callbacks : une reentrance volontaire et controlee](10-flashloan.md)
11. [setAuthorization et setAuthorizationWithSig : deleguer sa position](11-autorisation.md)
12. [Une gouvernance minimale : approuver des briques, jamais des marches](12-gouvernance.md)
13. [Limites connues et perimetre de ce parcours](13-limites-et-perimetre.md)
