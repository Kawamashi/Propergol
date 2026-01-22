# Propergol, l’ergonomie sans compromis
 A SturdE-style keyboard layout for French-speaking typists and programmers.

![layout](https://github.com/Kawamashi/Propergol/blob/main/Propergol2.png)

## Présentation
Propergol est une disposition de clavier pour le français et l’anglais dont le but est d’être la plus ergonomique possible. Pour ça, elle tire parti de toutes les possibilités offertes par les claviers ergo programmables, que ce soit au niveau de leur géométrie (avec leurs quatre touches de pouce au minimum) ou des possibilités offertes par leur firmware programmable. 

Je voulais que Propergol soit extrêmement confortable, avec une heatmap et une charge des doigts très équilibrée et particulièrement peu de difficultés (bigrammes à un doigt, ciseaux, extensions latérales et mauvaises redirections). La disposition privilégie les roulements pour une expérience de frappe fluide, et plus particulièrement les roulements vers l’intérieur, les plus confortables. Elle minimise les redirections et les longues séquences tapées avec une seule main, qui fatiguent inutilement l’une des deux mains. Par conséquent, la frappe rebondit naturellement entre les deux mains. Elle reste “régulière” et rythmée.

Je voulais également avoir les caractères les plus utilisés en français en accès direct, notamment É, À, È et l’apostrophe.

* [Contexte](#contexte)
* [Détail des solutions employées](#Détail-des-solutions-employées)
* [La touche morte de Propergol](#La-touche-morte-de-Propergol)
* [Propergol pour la programmation](#Propergol-pour-la-programmation)
* [Quelques choix de conception](#Quelques-choix-de-conception)
* [Variantes](#Variantes)

## Contexte
Les dispositions alternatives équilibrent bien mieux la charge des doigts que l’AZERTY ou le QWERTY. Malgré ça, elles n’évitent pas la surcharge d’un doigt, comme l’index gauche en Bépo, le majeur de la même main en Ergo-L ou l’annulaire droit dans la plupart des layouts alternatifs modernes anglophones (Gallium, Graphite, Sturdy, etc).  Cette surcharge est inévitable, elle est principalement due au placement du E, lettre la plus utilisée en français et en anglais. 

De même, ces dispositions améliorent beaucoup le confort de frappe, en diminuant drastiquement la quantité de bigrammes à un doigt (SFB), de ciseaux, d’extensions latérales (LSB) et de mauvaises redirections en comparaison avec les dispositions historiques. Cependant, arrivé à un certain degré d’optimisation, il devient impossible de descendre en dessous d’un certain plancher de difficultés sans déséquilibrer le layout. De plus, ces dispositions ne peuvent pas éviter les répétitions de même touche (SKB). 

La seule solution pour optimiser davantage le layout est de changer l’un des postulats de base, à savoir la compatibilité avec un clavier standard. À ce titre, Propergol propose : 
-	d’utiliser quatre touches de pouce au lieu de la seule barre d’espace
-	d’intégrer une touche Repeat et une touche magique
-	d’exploiter les possibilités offertes par les Clever Keys, qui rendent le layout adaptatif.

&nbsp;</br>

## Détail des solutions employées
L’utilisation des touches de pouce présente de nombreux avantages. En premier lieu, la disposition gagne une touche de repos. Le E était le candidat naturel vu sa fréquence d’utilisation en français comme en anglais. Son placement sous un pouce permet de mieux équilibrer la charge de tous les doigts. De plus, avoir une touche sous un pouce fait mécaniquement diminuer les SFB, les ciseaux et les mauvaises redirections.

Propergol utilise la touche Repeat et la touche Alt-Repeat de QMK. La touche Repeat permet de répéter la dernière touche tapée. En la mettant sous un pouce, on transforme tous les SKB en roulements vers l’intérieur, l’enchainement le plus confortable ! 

La touche Alt-Repeat produit un caractère en fonction de la lettre qui a été tapée avant. Propergol utilise Alt-Repeat comme une touche magique, pour éliminer les bigrammes les plus pénalisants de la disposition. Pour aller plus loin, cette touche peut aussi servir de raccourci pour des enchainements particulièrement fréquents (`ION`, `MENT`).

Enfin, les Clever Keys étendent le concept de touche magique à tout le layout. Je m’en sers par exemple :
-	pour ajouter automatiquement le `U` entre `Q` et une voyelle (ou une apostrophe)
-	pour mettre automatiquement la première lettre d’une phrase en majuscule
  
Ces fonctionnalités permettent d’éliminer la totalité des SKB, la majeure partie des SFB (seulement 0.35 % en français et 0.4 % en anglais), des redirections fréquentes et des ciseaux.

Cependant, il y a une contrepartie. On se débarrasse des enchainements inconfortables en utilisant des touches autres que celles qui produisent le caractère habituellement. Par exemple, `U` et `I` sont sur la même colonne. Pour que `UI` ne soit pas un SFB, il faut utiliser la touche magique pour taper I. Cela crée une charge cognitive. Il ne faut donc pas abuser de ces touches alternatives. Pour fonctionner correctement, Propergol a besoin de 7 règles magiques :
-	`U` + `Magic` → `UI` : transforme le SFB `UI` en bigramme vers l’intérieur
-	`Q` + voyelle / apostrophe → insère le `U` automatiquement pour éviter le ciseau `QU` et diminue de moitié les occurrences de `UI` (dues à `QUI`).
-	`Q` + `Magic` → `QUÉ` : transforme le ciseau `QÉ` en bigramme vers l’intérieur
-	`Q` + `H` → `QUOI` : transforme presque tous les SFB `QO` en bigrammes vers l’intérieur
-	`S` + `Magic` → `SC` : transforme le SFB `SC` en bigramme vers l’intérieur
-	`P` + `Magic` → `PH` : transforme le SFB `PH` en bigramme vers l’intérieur 
-	`N` + `Magic` → `N`. : transforme le SFB `PH` en bigramme vers l’intérieur 

Pour aller plus loin, voilà des règles optionnelles qui améliorent davantage la disposition :
-	`Q` + `N` → `QUAND`
-	`I` + `Magic` → `ION`
-	`M` (si précédé d’une lettre) + `Magic` → `MENT`
-	`M` + `Magic` (sinon) → `MÊME`
-	`É` + `Magic` → `ÉA`
-	`P` + `C` → `PAS`
-	`P` + `J` → `POUR`
-	`C` + `M` → `CH`
-	`Y` + `Magic` → `Y,`
-	`Y` + `È` → `YOU`
-	`C` + `J` → `CK`
  
Au fur et à mesure de la pratique, l’utilisation des touches alternatives devient de plus en plus naturelle, et la charge cognitive diminue. 

&nbsp;</br>

## La touche morte de Propergol
Propergol utilise une touche morte de type Lafayette pour taper tous les caractères accentués ainsi que les caractères spéciaux :
-	`★` + voyelle → voyelle avec circonflexe
-	`★` + `espace` → `_` (tiret bas). 
-	Tous les caractères d’Ergo‑L sont présents sur Propergol
-	Les différents guillemets doubles sont dans le pavé 3×10
-	`★` + `-` (signe moins) → `−` (signe moins typographique)
-	`★` + trait d’union → trait d’union insécable
-	`★` + `Q` → `Q`, sans que le `U` soit inséré automatiquement après (pour écrire `Qatar` par ex)
-	`★` + `T` → `/`
-	etc.
  
Propergol repousse les limites de la touche morte en l’implémentant comme une couche QMK, accessible avec un one-shot layer. De cette manière : 
-	l’utilisateur peut personnaliser la couche 1DK sans avoir besoin de retoucher le driver 
-	la touche morte peut être annulée par un autre appui sur celle-ci
-	les caractères de la couche morte peuvent être enchaînés par un appui prolongé sur la touche 1DK
-	la touche Repeat est capable de répéter un caractère de la couche 1DK
-	on peut rendre la couche 1DK compatible avec d’autres fonctionnalités de QMK, comme Caps Word, les Clever Keys, etc.
-	si l’utilisateur le souhaite, `shift` + `1DK` peut s’appliquer au caractère suivant la touche morte. Par exemple, pour taper `Ô`, on peut faire `shift` + `1DK` + `O`.

&nbsp;</br>

## Pour le français
J’aime beaucoup l’approche Lafayette, mais je voulais que les caractères les plus fréquents soient en accès direct, notamment `É`, `È`, `À` et l’apostrophe. En contrepartie, j’ai accepté de mettre le `Z` en couche 1DK. 

De base, l’apostrophe est située sur la couche 1DK, au même endroit que la touche Repeat. Néanmoins, on peut optimiser les choses en français. En effet, les occurrences de répétitions de lettres et de l’apostrophe y sont mutuellement exclusives. La touche `Repeat` est donc configurée pour donner une apostrophe lorsque la répétition de la dernière lettre est improbable.

De la même manière, la touche magique de Propergol est configurée pour produire `À` par défaut. `À` n’est employé qu’après un `L` (`là`, `delà`), un `J` (`déjà`), un `Ç` (`deçà`) ou si le caractère précédent n’est pas une autre lettre. Propergol n’utilise donc pas de règle magique commençant par `L`, `J` et `Ç` afin d’avoir `À` en accès direct. En backup, `À` est au même emplacement sur la couche 1DK.

L’usage de la touche 1DK est donc très réduit avec Propergol, aux alentours de 0.6 %. 

&nbsp;</br>

## Propergol pour la programmation

![symbols](https://github.com/Kawamashi/Propergol/blob/main/Propergol_symboles.png)

Propergol utilise une couche de programmation inspirée de celle d’Ergo-L, accessible également avec Alt-gr. Cette dernière est très bien pensée, mais certaines choses me gênent un peu. Propergol propose une alternative, avec :
-	les délimiteurs `()` `[]` `{}` en bloc sur la main gauche
-	`<>` et `^$` sur la main gauche également
-	les symboles arithmétiques en ligne, sur la home-row, avec `/` en position de repos de l’index
-	-	`"` et `'` facilement accessibles, sous l’index également
-	 `;` en position de repos de l’autre index
-	un bloc pour les opérateurs booléens `&` `|` `~`
-	les symboles peu courants (`%` `#` `^` `@` `~`) dans les coins ou sur les colonnes intérieures

Les enchainements de symboles les plus courants sont confortables. Par exemple : 
-	`()` `[]` `{}` `<>` : roulements vers l’intérieur
-	`);` : roulement vers l’intérieur
-	`!=` et `+=` : roulements vers l’intérieur
-	`>=` et `<=` : alternance
-	`->` et `<-` : alternance
-	`/*` et `*/` : roulements
-	`";` : alternance
-	`~/` : roulement vers l’intérieur
-	`</` : alternance
-	`["]` : alternance



Si vous préférez la couche de symboles d’Ergo-L, ce n’est pas un souci. Il vous suffit d’éditer le .toml de Propergol pour remplacer la couche Alt-gr par celle d’Ergo-L. Kalamine vous créera votre driver personnalisé en deux temps trois mouvements !

&nbsp;</br>

## Quelques choix de conception
Pour minimiser les redirections, toutes les voyelles sont placées du même côté. Pour garder une heatmap et une charge des doigts équilibrée d’une part, et ne pas faire exploser les SFB d’autre part, il faut mettre une consonne sous l’index côté voyelles. Le choix s’est rapidement porté sur le `N`. En effet, avoir le `N` côté voyelles permet d’avoir tous les “sons voyelles”, y compris `ON`, `AN`, `IN`, `UN` et `EN`, sur la même moitié de clavier. De plus, `N` est une lettre “directive” : il y a quatre fois plus de bigrammes où `N` suit une voyelle que de bigrammes où une voyelle suit un `N`. Avec `N` sous l’index, la disposition a naturellement tendance à rouler vers l’intérieur.

Toujours pour favoriser les roulements vers l’intérieur tout en équilibrant la charge des doigts, le `I` et le `U` doivent être placés sous le majeur. Cela pose moins problème que ce qu’on pourrait penser. En effet, `IU` est un bigramme extrêmement rare. On peut donc l’ignorer et se concentrer sur `UI`. Quand on analyse le corpus, la moitié des occurrences de `UI` vient de `QUI`. Avec l’insertion automatique du `U` entre `Q` et `I`, le nombre d’occurrences de `UI` est donc divisé par deux. En définitive, ce SFB se gère facilement avec la touche magique, sans provoquer de charge cognitive excessive.

Grâce à ces deux choix de conception, toutes les voyelles sont sur la même moitié du clavier, et tous les sons voyelles (`OI`, `AI`, `AU`, `AI`, `ON`, `AN`, `IN`, etc) se font en roulements vers l’intérieur. Je trouve ça logique et super confortable !

Je ne connais pas d’autres layouts ayant `L` sur la rangée de repos. C’est un choix logique, étant donné que `L` est la 9e lettre la plus employée en français, et la 10e en anglais. Cela dit, `L` est l’une des lettres les plus fréquemment doublées dans les deux langues, ce qui n’est pas confortable quand il faut le faire avec l’auriculaire. La touche `Repeat` répond à cette problématique.

&nbsp;</br>

## Variantes
Je préfère la position basse de l’auriculaire (le `Z` de QWERTY) à la position haute (le `Q` de QWERTY), mais pour certaines personnes c’est l’inverse. Dans ce cas, les touches des auriculaires peuvent être inversées sans souci, en adaptant quelques règles magiques :
-	`QÉ` (qui donne `QUÉ`) n’est plus un ciseau, la règle correspondante ne sert plus à rien
-	`Q` + `P` → `QUOI` (au lieu de `Q` + `H`)
-	La règle `M` + `Magic` → `MÊME` n’est plus nécessaire, même si l’utilisateur peut la conserver
  
De même, l’inversion du tiret et du B est tout à fait envisageable, même si cela implique de ne plus avoir les parenthèses de la couche 1DK symétriques (celles de la couche symboles ne sont pas modifiées). Dans ce cas, il faudra retoucher légèrement la couche 1DK pour éviter les ciseaux sur la main droite.

Est-ce que Propergol peut fonctionner avec moins de 30 touches sur le pavé principal ? 

Je n’aime pas les touches d’index basses sur les colonnes intérieures. Je ne les utilise pas sur mes claviers. Propergol fonctionne bien sans ces touches, il suffit de mettre B et K sur la couche 1DK et de remanier celle-ci en fonction. Voilà à quoi ressemble ma configuration :

J’ai essayé de faire rentrer Propergol sur les claviers type Hummingbird, avec seulement deux touches sous les auriculaires. Je n’ai pas trouvé de solution satisfaisante, je bloque notamment sur la virgule. N’hésitez pas à me contacter si vous avez des idées !

