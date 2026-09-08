# Chapitre 12 — Une gouvernance minimale : approuver des briques, jamais des marches

Le role `owner` de Morpho Blue est deliberement restreint. Il ne peut ni approuver un marche specifique, ni geler des fonds, ni modifier les parametres d'un marche deja cree : les seules actions possibles sont `enableIrm` (ajouter un contrat de modele de taux a la liste blanche), `enableLltv` (ajouter une valeur de seuil de liquidation autorisee, sous le plafond `WAD` soit 100 %), `setFee` (fixer les frais d'un marche existant, plafonnes a `MAX_FEE`) et `setFeeRecipient` (designer qui recoit ces frais).

Cette conception fait de Morpho Blue un protocole quasi immuable au sens ou aucune action de gouvernance ne peut jamais modifier retroactivement les regles d'un marche deja actif : une fois qu'un marche existe avec son LLTV, son oracle et son IRM, ces trois parametres sont graves pour toujours dans son `Id`. La seule ressource que la gouvernance controle est la liste des briques (IRM et LLTV) disponibles pour **de futurs** marches, jamais les marches existants.

`extSloads` complete ce tableau : une fonction de lecture generique qui expose n'importe quel emplacement de stockage brut du contrat par son slot, utile pour des integrations off-chain ou d'autres contrats qui ont besoin de lire l'etat interne de Morpho Blue sans dependre de getters specifiques — une facade de lecture minimaliste, coherente avec la philosophie generale du contrat.

[Chapitre suivant : limites et perimetre](13-limites-et-perimetre.md)
