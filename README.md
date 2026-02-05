# Propergol, l’ergonomie sans compromis
 A SturdE-style keyboard layout for French-speaking typists and programmers.

![layout](https://github.com/Kawamashi/Propergol/blob/main/Propergol2.png)

Propergol est une disposition de clavier pour le français et l’anglais dont le but est d’être la plus ergonomique possible. Pour ça, elle tire parti de toutes les possibilités offertes par les claviers ergo programmables, que ce soit au niveau de leur géométrie (avec leurs quatre touches de pouce au minimum) ou des possibilités offertes par leur firmware programmable. 

Je voulais que Propergol soit extrêmement confortable, avec une heatmap et une charge des doigts très équilibrée et particulièrement peu de difficultés (bigrammes à un doigt, ciseaux, extensions latérales et mauvaises redirections). La disposition privilégie les roulements pour une expérience de frappe fluide, et plus particulièrement les roulements vers l’intérieur, les plus confortables. Elle minimise les redirections et les longues séquences tapées avec une seule main, qui fatiguent inutilement l’une des deux mains. Par conséquent, la frappe rebondit naturellement entre les deux mains. Elle reste “régulière” et rythmée.

Je voulais également avoir les caractères les plus utilisés en français **en accès direct**, notamment `É`, `À`, `È` et l’apostrophe.

* [Contexte](#contexte)
* [Détail des solutions employées](#Détail-des-solutions-employées)
* [La touche morte de Propergol](#La-touche-morte-de-Propergol)
* [Pour le français et l'anglais](#Pour-le-français-et-langlais)
* [Propergol pour la programmation](#Propergol-pour-la-programmation)
* [Quelques choix de conception](#Quelques-choix-de-conception)
* [Variantes](#Variantes)

## Contexte
Les dispositions alternatives équilibrent bien mieux la charge des doigts que l’AZERTY ou le QWERTY. Malgré ça, elles n’évitent pas la surcharge d’un doigt, comme l’index gauche en Bépo, le majeur de la même main en [Ergo-L](https://ergol.org/) ou l’annulaire droit dans la plupart des layouts alternatifs modernes anglophones ([Gallium](https://github.com/GalileoBlues/Gallium), [Graphite](https://github.com/rdavison/graphite-layout), [Sturdy](https://oxey.dev/sturdy/index.html), etc).  Cette surcharge est inévitable, elle est principalement due au placement du `E`, lettre la plus utilisée en français et en anglais. 

De même, ces dispositions améliorent beaucoup le confort de frappe, en diminuant drastiquement la quantité de bigrammes à un doigt (SFB), de ciseaux, d’extensions latérales (LSB) et de mauvaises redirections en comparaison avec les dispositions historiques. Cependant, arrivé à un certain degré d’optimisation, il devient impossible de descendre en dessous d’un certain plancher de difficultés sans déséquilibrer le layout. De plus, ces dispositions ne peuvent pas éviter les répétitions de même touche (SKB). 

La seule solution pour optimiser davantage le layout est de changer l’un des postulats de base, à savoir la compatibilité avec un clavier standard. À ce titre, Propergol propose : 
-	d’utiliser quatre touches de pouce au lieu de la seule barre d’espace
-	d’intégrer une touche *Repeat* et une touche magique
-	d’exploiter les possibilités offertes par les *Clever Keys*, qui rendent le layout adaptatif.

&nbsp;</br>

## Détail des solutions employées
L’utilisation des touches de pouce présente de nombreux avantages. En premier lieu, la disposition gagne une touche de repos. Le `E` était le candidat naturel vu sa fréquence d’utilisation en français comme en anglais. Son placement sous un pouce permet de mieux équilibrer la charge de tous les doigts. De plus, avoir une touche sous un pouce fait mécaniquement diminuer les SFB, les ciseaux et les mauvaises redirections.

Propergol utilise la touche [*Repeat*](https://docs.qmk.fm/features/repeat_key) et la touche [*Alt-Repeat*](https://docs.qmk.fm/features/repeat_key#alternate-repeating) de QMK. La touche *Repeat* permet de répéter la dernière touche tapée. En la mettant sous un pouce, on transforme tous les SKB en roulements vers l’intérieur, l’enchainement le plus confortable ! 

La touche *Alt-Repeat* `⚝` produit un caractère en fonction de la lettre qui a été tapée avant. Propergol l’utilise comme une touche magique, pour éliminer les bigrammes les plus pénalisants de la disposition. Pour aller plus loin, cette touche peut aussi servir de raccourci pour des enchainements particulièrement fréquents (`ION`, `MENT`).

Enfin, les [Clever Keys](https://github.com/Kawamashi/qmk_userspace/blob/main/README.md#clever-keys) étendent le concept de touche magique à tout le layout. On peut s’en servir par exemple :
-	pour ajouter automatiquement le `U` entre `Q` et une voyelle (ou une apostrophe)
-	pour mettre automatiquement la première lettre d’une phrase en majuscule
-	pour donner des effets “magiques” à n’importe quelle touche, pas seulement la touche *Alt-Repeat*
-	pour paramétrer plus finement cette dernière, en tenant compte de la série de touches tapées avant et non pas seulement de la dernière
  
Ces fonctionnalités permettent d’éliminer la totalité des répétitions de caractères, la majeure partie des SFB (seulement 0.35 % en français et 0.4 % en anglais), des redirections fréquentes et des ciseaux.

Cependant, il y a une contrepartie. On se débarrasse des enchainements inconfortables en utilisant des touches autres que celles qui produisent le caractère habituellement. Par exemple, `U` et `I` sont sur la même colonne. Pour que `UI` ne soit pas un SFB, il faut utiliser la touche magique pour taper `I`. Cela crée une charge cognitive. Il ne faut donc pas abuser de ces touches alternatives.  

De base, Propergol utilise 7 règles magiques :
-	`U` `⚝` → `UI` : transforme le SFB `UI` en bigramme vers l’intérieur
-	`Q` suivi d’une voyelle ou d’une apostrophe → insère le `U` automatiquement pour éviter le ciseau `QU` et diminue de moitié les occurrences de `UI` (dues à `QUI`).
-	`Q` `H` → `QUOI` : transforme presque tous les SFB `QO` en bigrammes vers l’intérieur
-	`S` `⚝` → `SC` : transforme le SFB `SC` en bigramme vers l’intérieur
-	`P` `⚝` → `PH` : transforme le SFB `PH` en bigramme vers l’intérieur 
-	`N` `⚝` → `N.` : transforme le SFB `N.` en bigramme vers l’intérieur
- `Y` `⚝` → `YI` : transforme le SFB `YI` en bigramme vers l’intérieur

Si à l’usage certaines de ces règles ne vous paraissent pas naturelles, ce n’est pas grave ! Personnellement je me passe des deux dernières sans aucun souci. Je dirais que Propergol a besoin des trois premières pour fonctionner confortablement.

Si vous voulez aller plus loin, voilà des règles optionnelles qui améliorent davantage la disposition :
-	`Q` `⚝` → `QUÉ`
-	`Q` `N` → `QUAND`
-	`I` `⚝` → `ION`
-	`M` (si précédé d’une lettre) + `⚝` → `MENT`
-	`M` `⚝` (sinon) → `MÊME`
-	`É` `⚝` → `ÉA`
-	`P` `C` → `PAS`
-	`P` `J` → `POUR`
-	`C` `M` → `CH`
-	`Y` `⚝` → `Y,`
-	`Y` `È` → `YOU`
-	`C` `J` → `CK`

Au fur et à mesure de la pratique, l’utilisation des touches alternatives devient de plus en plus naturelle, et la charge cognitive diminue. 

&nbsp;</br>

## La touche morte de Propergol
Propergol utilise une [touche morte de type Lafayette](https://ergol.org/presentation/#impeccable-en-fran%C3%A7ais) `★` pour taper les caractères accentués, les diacritiques ainsi que les symboles typographiques :
-	`★` suivi d’une voyelle → voyelle avec circonflexe
-	`ç` est en dessous du `c`, `œ` et `æ` sont au-dessus de `o` et `a` respectivement
-	`★` `espace` → `_` (tiret bas)
-	Les différents guillemets doubles sont dans le pavé 3×10
-	`★` `-` (signe moins) → `−` (signe moins typographique)
-	`★` suivi d’un trait d’union → trait d’union insécable
-	`★` `Q` → `Q`, sans que le `U` soit inséré automatiquement après (pour écrire `Qatar` par ex)
-	`★` `T` → `/`
-	etc.
  
Propergol repousse les limites de la touche morte en l’implémentant comme une couche QMK, accessible avec un [one-shot layer](https://docs.qmk.fm/one_shot_keys). De cette manière : 
-	l’utilisateur peut personnaliser la couche 1DK sans avoir besoin de retoucher le driver 
-	la touche morte peut être annulée par un autre appui sur celle-ci
-	les caractères de la couche morte peuvent être enchaînés par un appui prolongé sur la touche 1DK
-	la touche Repeat est capable de répéter un caractère de la couche 1DK
-	on peut rendre la couche 1DK compatible avec d’autres fonctionnalités de QMK, comme [Caps Word](https://docs.qmk.fm/features/caps_word), les Clever Keys, etc.
-	si l’utilisateur le souhaite, `shift` + `1DK` peut s’appliquer au caractère suivant la touche morte. Par exemple, pour taper `Ô`, on peut faire `shift` + `1DK` + `O`.

&nbsp;</br>

## Pour le français et l’anglais
Propergol a été conçu pour que la frappe soit la plus confortable possible, dans les deux langues. Pour permettre cela, le `H` (9e lettre la plus fréquente en anglais) et le `U` (8e lettre la plus fréquente en français) n’ont pas été placées sur la rangée de repos, mais sur des touches néanmoins très accessibles. Grâce à ce compromis, la heatmap et la charge des doigts sont équilibrées dans les deux langues. 

Les enchainements de lettres ont été étudiés de manière à créer le moins de difficultés possibles (bigrammes à un doigt, ciseaux, extensions latérales et mauvaises redirections). Grâce à l’usage des touches de pouce, des touches Repeat et Magic ainsi que des Clever Keys, Propergol contient ces difficultés à un niveau plancher :

&nbsp;</br>

<table>
  <thead>
    <tr>
      <th rowspan="2">Langue</th>
      <th rowspan="2">Layout</th>
      <th colspan="3">Same Finger</th>
      <th rowspan="2">LSB</th>
      <th colspan="3">Ciseaux</th>
      <th colspan="3">Redirections</th>
      <th rowspan="2">CC</th>
    </tr>
    <tr>
      <th>SFB</th>
      <th>SFS</th>
      <th>STS</th>
      <th>FSB</th>
      <th>HSB</th>
      <th>RJB</th>
      <th>Total</th>
      <th>Bad Redir</th>
      <th>SHS</th>
    </tr>
  </thead>
   <tr>
    <td colspan ="13"> </td>
   </tr>
   <tr>
    <th rowspan="5">Français</th>
    <th>Propergol base</th>
    <td>0.39 %</td>
    <td>3.71 %</td>
    <td>1.20 %</td>
    <td>1.12 %</td>
    <td>0.09 %</td>
    <td>2.37 %</td>
    <td>0.44 %</td>
    <td>7.46 %</td>
    <td>0.24 %</td>
    <td>2.54 %</td>
    <td>4.98 %</td>
   </tr>
   <tr>
    <th>Propergol + options</th>
    <td>0.36 %</td>
    <td>3.79 %</td>
    <td>1.24 %</td>
    <td>1.12 %</td>
    <td>0.08 %</td>
    <td>2.00 %</td>
    <td>0.31 %</td>
    <td>5.56 %</td>
    <td>0.21 %</td>
    <td>2.44 %</td>
    <td>6.35 %</td>
   </tr>
   <tr>
    <th>Ergo-L</th>
    <td>1.18 %</td>
    <td>5.10 %</td>
    <td>0.00 %</td>
    <td>1.90 %</td>
    <td>0.21 %</td>
    <td>4.70 %</td>
    <td>0.87 %</td>
    <td>10.79 %</td>
    <td>2.10 %</td>
    <td>7.76 %</td>
    <td>3.57 %</td>
   </tr>
    <tr>
    <th>Erglace</th>
    <td>0.89 %</td>
    <td>4.99 %</td>
    <td>0.00 %</td>
    <td>1.31 %</td>
    <td>0.23 %</td>
    <td>2.88 %</td>
    <td>1.02 %</td>
    <td>4.13 %</td>
    <td>0.31 %</td>
    <td>2.76 %</td>
    <td>3.58 %</td>
   </tr>
   <tr>
    <td colspan ="12"> </td>
   </tr>
   <tr>
    <td colspan ="13"> </td>
   </tr>
   <tr>
    <th rowspan="5">Anglais</th>
    <th>Propergol base</th>
    <td>0.42 %</td>
    <td>5.49 %</td>
    <td>0.82 %</td>
    <td>1.93 %</td>
    <td>0.12 %</td>
    <td>2.56 %</td>
    <td>0.73 %</td>
    <td>8.94 %</td>
    <td>0.97 %</td>
    <td>2.95 %</td>
    <td>2.86 %</td>
   </tr>
   <tr>
    <th>Propergol + options</th>
    <td>0.42 %</td>
    <td>4.87 %</td>
    <td>0.83 %</td>
    <td>1.68 %</td>
    <td>0.13 %</td>
    <td>2.07 %</td>
    <td>0.48 %</td>
    <td>6.71 %</td>
    <td>0.16 %</td>
    <td>2.66 %</td>
    <td>3.94 %</td>
   </tr>
   <tr>
    <th>Ergo-L</th>
    <td>1.39 %</td>
    <td>7.32 %</td>
    <td>0.00 %</td>
    <td>4.61 %</td>
    <td>0.19 %</td>
    <td>4.92 %</td>
    <td>1.08 %</td>
    <td>13.65 %</td>
    <td>2.29 %</td>
    <td>8.45 %</td>
    <td>0.58 %</td>
   </tr>
   <tr>
    <th>Erglace</th>
    <td>1.32 %</td>
    <td>5.66 %</td>
    <td>0.00 %</td>
    <td>2.98 %</td>
    <td>0.18 %</td>
    <td>4.70 %</td>
    <td>1.33 %</td>
    <td>3.35 %</td>
    <td>0.39 %</td>
    <td>0.65 %</td>
    <td>0.96 %</td>
   </tr>
   <tr>
    <th>Sturdy</th>
    <td>0.86 %</td>
    <td>5.10 %</td>
    <td>0.00 %</td>
    <td>4.11 %</td>
    <td>0.31 %</td>
    <td>3.03 %</td>
    <td>1.54 %</td>
    <td>6.15 %</td>
    <td>0.35 %</td>
    <td>2.66 %</td>
    <td>0.00 %</td>
   </tr>
</table>
&nbsp;</br>

Ces statistiques sont issues de [Kawalyser](https://github.com/Kawamashi/Kawalyser). Vous trouverez [ici](https://github.com/Kawamashi/Kawalyser/blob/main/Glossaire.md) un glossaire de toutes les abréviations utilisées dans le tableau.

&nbsp;</br>
Pour la typographie, tous les caractères d’Ergo‑L sont présents sur Propergol (majuscules accentuées, espaces insécables, apostrophe typographique, tirets cadratins, etc), notamment grâce à la touche morte.
J’aime beaucoup l’approche Lafayette, mais je voulais que les caractères les plus fréquents en français soient en accès direct, notamment `É`, `È`, `À` et l’apostrophe. Pour cela :

- `É` et `È` ont des touches dédiées.
- la touche `Repeat` produit une apostrophe quand on en a besoin en français. En effet, les occurrences de répétitions de lettres et de l’apostrophe y sont mutuellement exclusives. La touche `Repeat` est donc configurée pour donner une apostrophe lorsque la répétition de la dernière lettre est improbable. En backup, l’apostrophe est au même emplacement sur la couche 1DK.
- la touche magique de Propergol est configurée pour produire `À` par défaut. En effet, `À` n’est employé qu’après un `L` (`là`, `delà`), un `J` (`déjà`), un `Ç` (`deçà`) ou si le caractère précédent n’est pas une autre lettre. Propergol n’utilise donc pas de règle magique commençant par `L`, `J` et `Ç` afin d’avoir `À` en accès direct. En backup, `À` est au même emplacement sur la couche 1DK.
- le `Z` passe en couche 1DK, en position de repos de l’index gauche.

L’usage de la touche 1DK est donc très réduit avec Propergol, aux alentours de 0.6 %. 

&nbsp;</br>

## Propergol pour la programmation

![symbols](https://github.com/Kawamashi/Propergol/blob/main/Propergol_symboles.png)

Propergol utilise une couche de programmation inspirée de celle d’Ergo-L, accessible également avec `Alt-gr`. Cette dernière est très bien pensée, mais certaines choses me gênent un peu. Propergol propose une alternative, avec :
-	les délimiteurs `()` `[]` `{}` en bloc sur la main gauche
-	`<>` et `^$` sur la main gauche également
-	les symboles arithmétiques `/` `-` `+` `*` sur la home-row de la main droite, avec `/` en position de repos de l’index
- `"` et `'` facilement accessibles, avec l’index également
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

Enfin, le tiret bas `_` est particulièrement accessible (`★` `espace`).



Si vous préférez la couche de symboles d’Ergo-L, ce n’est pas un souci. Il vous suffit d’éditer le .toml de Propergol pour remplacer la couche Alt-gr par celle d’Ergo-L. [Kalamine](https://github.com/OneDeadKey/kalamine) vous créera votre driver personnalisé en deux temps trois mouvements !

&nbsp;</br>

## Quelques choix de conception
Pour minimiser les redirections, toutes les voyelles sont placées du même côté. Pour garder une heatmap et une charge des doigts équilibrée d’une part, et ne pas faire exploser les SFB d’autre part, il faut mettre une consonne sous l’index côté voyelles. Le choix s’est rapidement porté sur le `N`. En effet, avoir le `N` côté voyelles permet d’avoir tous les “sons voyelles”, y compris `ON`, `AN`, `IN`, `UN` et `EN`, sur la même moitié de clavier. De plus, `N` est une lettre “directive” : il y a quatre fois plus de bigrammes où `N` suit une voyelle que de bigrammes où une voyelle suit un `N`. Avec `N` sous l’index, la disposition a naturellement tendance à rouler vers l’intérieur.

Toujours pour favoriser les roulements vers l’intérieur tout en équilibrant la charge des doigts, le `I` et le `U` doivent être placés sous le majeur. Cela pose moins problème que ce qu’on pourrait penser. En effet, `IU` est un bigramme extrêmement rare. On peut donc l’ignorer et se concentrer sur `UI`. Quand on analyse le corpus, la moitié des occurrences de `UI` vient de `QUI`. Avec l’insertion automatique du `U` entre `Q` et `I`, le nombre d’occurrences de `UI` est donc divisé par deux. En définitive, ce SFB se gère facilement avec la touche magique, sans provoquer de charge cognitive excessive.

Grâce à ces deux choix de conception, toutes les voyelles sont sur la même moitié du clavier, et tous les sons voyelles (`OI`, `AI`, `AU`, `AI`, `ON`, `AN`, `IN`, etc) se font en roulements vers l’intérieur. Je trouve ça logique et super confortable !

Je ne connais pas d’autres layouts ayant `L` sur la rangée de repos. C’est pourtant un choix logique, étant donné que `L` est la 10e lettre la plus employée en français, et la 11e en anglais. Cela dit, `L` est l’une des lettres les plus fréquemment doublées dans les deux langues, ce qui n’est pas confortable quand il faut le faire avec l’auriculaire. La touche `Repeat` répond à cette problématique.

&nbsp;</br>

## Variantes
Je préfère la position basse de l’auriculaire (le `Z` de QWERTY) à la position haute (le `Q` de QWERTY), mais pour certaines personnes c’est l’inverse. Dans ce cas, les touches des auriculaires peuvent être inversées sans souci, en adaptant quelques règles magiques :
-	`QÉ` (qui donne `QUÉ`) n’est plus un ciseau, la règle correspondante ne sert plus à rien
-	`Q` + `P` → `QUOI` (au lieu de `Q` + `H`)
-	La règle `M` + `⚝` → `MÊME` n’est plus nécessaire, même si l’utilisateur peut la conserver
  
De même, l’inversion du tiret et du B est tout à fait envisageable, même si cela implique de ne plus avoir les parenthèses de la couche 1DK symétriques (celles de la couche symboles ne sont pas modifiées). Dans ce cas, il faudra retoucher légèrement la couche 1DK pour éviter les ciseaux sur la main droite.

Est-ce que Propergol peut fonctionner avec moins de 30 touches sur le pavé principal ? 

Je n’aime pas les touches d’index basses sur les colonnes intérieures. Je ne les utilise pas sur mes claviers. Propergol fonctionne bien sans ces touches, il suffit de mettre B et K sur la couche 1DK et de remanier celle-ci en fonction. Voilà à quoi ressemble ma configuration :



J’ai essayé de faire rentrer Propergol sur les claviers type Hummingbird, avec seulement deux touches sous les auriculaires. Je n’ai pas trouvé de solution satisfaisante, je bloque notamment sur la virgule. N’hésitez pas à me contacter si vous avez des idées !

