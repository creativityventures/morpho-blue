# Chapitre 1 — Presentation de Morpho Blue

Morpho Blue est un protocole de pret et emprunt qui pousse a l'extreme l'idee de marche isole : au lieu d'un pool unique partage entre de nombreux actifs (Aave, Compound v2) ou d'un actif de base entoure de collateraux (Compound v3), Morpho Blue est un contrat unique et non-custodial dans lequel n'importe qui peut creer, sans vote de gouvernance, un marche completement independant defini par cinq parametres : un jeton emprunte, un jeton de collateral, un oracle de prix, un modele de taux d'interet (IRM) et un seuil de liquidation (LLTV).

Chaque marche ainsi cree est totalement etanche aux autres : la dette d'un marche ne peut jamais affecter la solvabilite d'un autre, puisque chaque marche a sa propre comptabilite d'actifs et de parts. Le protocole lui-meme reste minimal et immuable une fois deploye ; toute la composition de risque (quel oracle faire confiance, quel LLTV choisir) est laissee a des couches au-dessus du protocole de base (des coffres tiers, hors perimetre de ce parcours).

Ce parcours s'appuie sur le depot cloné a la date d'ecriture. Le contrat entier tient dans un seul fichier, `src/Morpho.sol`, epaule par des bibliotheques dans `src/libraries/` (`MathLib`, `SharesMathLib`, `MarketParamsLib`, `SafeTransferLib`, `UtilsLib`, `ConstantsLib`) et des interfaces dans `src/interfaces/`.

Rien n'a ete installe, compile ni execute pour ecrire ces chapitres.

[Chapitre suivant : architecture en singleton et marches par hash](02-architecture.md)
