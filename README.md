## Ce que fait l'application

Quand on ouvre l'application, on voit un texte "Calculate Tip", une zone de texte appelée "Bill Amount" et un texte "Tip Amount" qui affiche le pourboire. On tape le montant de la facture dans la zone de texte, avec un clavier qui contient seulement des chiffres. L'application calcule alors 15 % de ce montant et l'affiche en dessous. Par exemple, si je tape 100, elle affiche Tip Amount: $15.00. Le symbole de la monnaie dépend de la langue du téléphone ou de l'émulateur.

## Comment ça marche

Tout le code est dans le fichier MainActivity.kt.

La fonction TipTimeLayout() construit l'écran. Elle contient une Column qui range les éléments les uns sous les autres : le texte "Calculate Tip", la zone de texte, le texte du pourboire et un espace vide à la fin.

La fonction EditNumberField() crée la zone de texte avec un TextField. Elle a un libellé "Bill Amount", elle reste sur une seule ligne et elle ouvre le clavier numérique.

La fonction calculateTip() calcule le pourboire. Elle prend le montant de la facture et un pourcentage qui vaut 15 par défaut. Elle multiplie le pourcentage divisé par 100 avec le montant, puis elle met le résultat au format d'une monnaie avec NumberFormat.

## Ce que j'ai appris sur l'état

L'état, c'est une valeur qui peut changer pendant que l'application tourne. Ici, c'est le montant que l'utilisateur tape, et je l'ai appelé amountInput.

Pour que Compose suive cette valeur, je l'ai créée avec mutableStateOf. Quand elle change, Compose redessine l'écran, et ça s'appelle la recomposition. Mais à chaque recomposition, la variable reviendrait à sa valeur de départ. C'est pour ça que j'ai utilisé remember, qui garde la valeur en mémoire entre deux recompositions.

Ensuite, j'ai fait ce qu'on appelle le hissage d'état. J'ai déplacé amountInput de EditNumberField() vers TipTimeLayout(). Comme ça, EditNumberField() n'a plus d'état à elle : elle reçoit la valeur avec le paramètre value et elle prévient TipTimeLayout() quand le texte change avec le paramètre onValueChange. Grâce à ça, TipTimeLayout() connaît le montant et peut calculer le pourboire pour l'afficher.

## Comment lancer le projet

J'ouvre le dossier du projet dans Android Studio, j'attends la fin de la synchronisation Gradle, puis je clique sur le bouton Run avec un émulateur ou un téléphone branché.

## Suite du projet

Pour l'instant, le pourcentage du pourboire est fixé à 15 %. Dans le prochain atelier, l'utilisateur pourra choisir lui-même ce pourcentage.
