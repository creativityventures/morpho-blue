# Chapitre 5 — supply et withdraw : le cote preteur du marche

`supply` accroit `position[id][onBehalf].supplyShares` et les totaux du marche, puis transfere le `loanToken` du preteur vers le contrat par `safeTransferFrom` — l'ordre des operations (mise a jour de l'etat avant le transfert) suit le motif checks-effects-interactions, renforce par le fait que le transfert est le tout dernier appel externe de la fonction. Un callback optionnel `onMorphoSupply` peut etre declenche avant ce transfert si l'appelant fournit des donnees (`data.length > 0`), permettant a un contrat appelant d'executer une logique personnalisee (par exemple emprunter ailleurs pour financer ce depot) avant que les fonds ne soient effectivement preleves.

`withdraw` fait l'inverse : parts brulees, totaux du marche reduits, puis `safeTransfer` des actifs vers `receiver`. Une seule verification de sante s'applique cote preteur, mais elle porte sur le marche entier et non sur le compte : `market[id].totalBorrowAssets <= market[id].totalSupplyAssets` doit rester vraie apres le retrait, ce qui revient a interdire de retirer plus de liquidite que ce que le marche a effectivement disponible (non pretee).

Contrairement au collateral (chapitre 7), la position de preteur n'entre dans aucun calcul de sante individuel : preter n'expose jamais un compte a une liquidation, seul emprunter le peut.

[Chapitre suivant : borrow, repay et le controle de sante](06-borrow-repay.md)
