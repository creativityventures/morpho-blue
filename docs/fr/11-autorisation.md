# Chapitre 11 — setAuthorization et setAuthorizationWithSig : deleguer sa position

Toutes les fonctions qui agissent au nom d'un compte tiers (`withdraw`, `borrow`, `withdrawCollateral`, `liquidate` indirectement via le solde vise) verifient `_isSenderAuthorized(onBehalf)`, qui n'autorise que le compte lui-meme ou une adresse explicitement approuvee via `isAuthorized[onBehalf][gestionnaire]`. `setAuthorization` permet d'accorder ou de revoquer cette delegation par une transaction directe.

`setAuthorizationWithSig` offre la meme delegation sans transaction prealable du compte proprietaire : une signature EIP-712 hors chaine, structuree autour d'un `Authorization` (autorisateur, autorise, booleen, nonce, date limite) et d'un domaine (`DOMAIN_SEPARATOR`, fixe une fois pour toutes a la construction du contrat a partir du chainId et de l'adresse du contrat), est verifiee sur chaine par recuperation de signature ECDSA. Le `nonce` par compte empeche qu'une meme signature soit rejouee deux fois.

Cette delegation est ce qui permet a des contrats tiers (des coffres de gestion automatisee, par exemple) d'agir pour le compte d'un utilisateur sur des positions Morpho Blue sans jamais detenir directement ses fonds : l'utilisateur garde la propriete de sa position, il delegue seulement le droit d'agir dessus.

[Chapitre suivant : la gouvernance minimale du protocole](12-gouvernance.md)
