# Chapitre 10 — flashLoan et les callbacks : une reentrance volontaire et controlee

`flashLoan` transfere un montant de n'importe quel jeton detenu par le contrat vers l'appelant, invoque `onMorphoFlashLoan` sur cet appelant, puis exige que les fonds soient rendus par un `safeTransferFrom` en fin d'appel : un pret sans garantie, rembourse dans la meme transaction, gratuit (aucun frais preleve), ouvert a n'importe quel jeton present dans le contrat plutot que limite au jeton d'un marche precis.

Ce motif de callback n'est pas reserve au flash loan : `supply`, `supplyCollateral`, `repay` et `liquidate` acceptent tous un parametre `data` optionnel qui, s'il est non vide, declenche un rappel vers l'appelant avant que le contrat ne preleve les fonds correspondants. Cela permet a un contrat integrateur d'executer une logique arbitraire (par exemple emprunter d'un cote pour rembourser de l'autre, ou echanger un actif contre un autre) au milieu d'une operation Morpho, sans avoir besoin d'enchainer plusieurs transactions separees.

Cette reentrance est volontaire et geree explicitement par la structure du code (l'etat est toujours mis a jour avant le rappel, jamais apres), plutot que bloquee par un verrou de reentrance global comme le `nonReentrant` deja rencontre dans les parcours precedents — un choix de conception qui echange une protection generique contre davantage de flexibilite pour les contrats qui integrent Morpho Blue.

[Chapitre suivant : setAuthorization et la delegation par signature](11-autorisation.md)
