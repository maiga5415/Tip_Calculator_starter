## Calculatrice
Je suis parti d'un code de démarrage fourni dans l'atelier, puis j'y ai ajouté les fonctionnalités qui manquaient.

## Ce que j'ai trouvé dans le code de départ

Le code de départ contenait déjà une partie de l'application. Dans le fichier strings.xml, il y avait les textes de l'application : le nom Tip Time, le libellé Calculate Tip, le libellé Bill Amount et le texte Tip Amount qui attend une valeur à afficher.

Dans le fichier MainActivity.kt, il y avait la fonction onCreate(), qui lance l'application et appelle TipTimeLayout() dans une Surface. Il y avait aussi la fonction TipTimeLayout(), qui contenait une Column avec deux textes, le texte Calculate Tip et le texte du pourboire, plus un Spacer pour laisser un espace vide. Le texte du pourboire affichait seulement $0.00 écrit en dur, donc il ne changeait jamais.

Il y avait aussi la fonction calculateTip(), qui calcule le pourboire avec un pourcentage de 15 par défaut et met le résultat au format d'une monnaie avec NumberFormat. Enfin, il y avait une fonction d'aperçu, TipTimeLayoutPreview(), pour voir l'écran dans Android Studio sans lancer l'application, et le thème de l'application déjà prêt.

## Ce que j'ai ajouté

J'ai créé la fonction EditNumberField(), qui affiche une zone de texte avec un TextField pour que l'utilisateur tape le montant de la facture. J'ai appelé cette fonction dans TipTimeLayout(), juste après le texte Calculate Tip.

J'ai ajouté un libellé Bill Amount dans la zone de texte, pour dire à l'utilisateur ce qu'il doit taper. J'ai mis singleLine à true pour que le texte reste sur une seule ligne, et j'ai configuré le clavier avec KeyboardOptions et KeyboardType.Number pour qu'il affiche seulement des chiffres.

J'ai ajouté l'état de l'application avec la variable amountInput, créée avec mutableStateOf pour que Compose suive ses changements, et avec remember pour qu'elle garde sa valeur quand l'écran se redessine. J'ai aussi ajouté les imports getValue et setValue pour pouvoir utiliser le mot by.

J'ai fait le hissage d'état. J'ai déplacé amountInput de EditNumberField() vers TipTimeLayout(), et j'ai donné à EditNumberField() les paramètres value et onValueChange. Comme ça, EditNumberField() n'a plus d'état à elle et TipTimeLayout() connaît le montant tapé.

Dans TipTimeLayout(), j'ai converti le texte tapé en nombre avec toDoubleOrNull() et l'opérateur Elvis, qui donne 0.0 quand le champ est vide ou invalide. Ensuite j'ai appelé calculateTip() avec ce montant et j'ai gardé le résultat dans la variable tip.

J'ai remplacé le $0.00 écrit en dur par la variable tip, pour que le pourboire s'affiche vraiment et change quand on tape un montant. Enfin, j'ai ajouté verticalScroll avec rememberScrollState dans la Column, pour que l'écran puisse défiler quand le clavier prend de la place.

## Comment ça marche

Quand l'utilisateur tape un montant, la fonction onValueChange met à jour amountInput. Comme c'est un état, Compose redessine l'écran, TipTimeLayout() recalcule le pourboire et le texte Tip Amount affiche la nouvelle valeur. Par exemple, si je tape 100, l'application affiche Tip Amount: $15.00. Le symbole de la monnaie dépend de la langue du téléphone ou de l'émulateur.

## Comment lancer le projet

J'ouvre le dossier du projet dans Android Studio, j'attends la fin de la synchronisation Gradle, puis je clique sur le bouton Run avec un émulateur ou un téléphone branché.

## Suite du projet

Pour l'instant, le pourcentage du pourboire est fixé à 15 %. Dans le prochain atelier, l'utilisateur pourra choisir lui-même ce pourcentage.
