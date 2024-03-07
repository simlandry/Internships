# Sujet de stage : étude de la résistance d'un algorithme de chiffrement symétrique contre la cryptanalyse

## Organisation du stage

|   Durée       |   Contenu |   Compétences acquises
|---            |---        |--- 
| Lundi am | Présentation cryptologie dans les puces Présentation du stage | Comprendre l'environnement de travail Notions de cryptologie | 
| Lundi pm - mardi am | Support python, papier/ordi, premier chiffrement symétrique (César) et tests | Bases en python, réflexion mathématique et algorithmique
| Mardi pm - jeudi pm | Réflexion contre-mesures, codes python et tests | Réflexion sur un sujet en cryptographie Autonomie
| Vendredi | Conclusion, présentation des résultats | Restitution des connaissances |

## Travailler avec Python

Lancer un interpréteur _python_ :
* Installer [Spyder](https://www.spyder-ide.org/)
* Sinon, lancer une console dans le navigateur : [console](https://pyodide.org/en/stable/console.html)

## Cours

* [Prérequis mathématiques](./prerequismaths.md)
* [Affichage](./affichage.md)
* [Type de Données](./typededonnees.md)
* [Variables](./variables.md)
* [Boucle For](./boucles.md)
* [Fonctions](./fonctions.md)
* [Conditions](./conditions/md)

## Chiffrement de César

### Définition

En cryptographie, le chiffre de César est une méthode de chiffrement par décalage des lettres de l'alphabet. Elle est utilisée par Jules César dans ses correspondances secrètes. Le texte chiffré s'obtient en remplaçant chaque lettre clair par une autre lettre unique de l'alphabet. Le nombre de positions décalées définit la clé secrète, utile pour chiffrer et déchiffrer. On est donc dans un type de chiffrement symétrique. Par exemple, avec un décalage de 3 vers la droite, la lettre A est remplacéee par D, B devient E, et ainsi jusqu'à W qui devient Z, puis X devient A, Y devient B et Z devient C. Il s'agit d'une permutation circulaire de l'alphabet. Dans le cas de l'alphabet latin, le chiffre de César n'a que 26 clés possibles (y compris la clé nulle qui ne modifie pas le texte clair). 

**Exemple**

Le chiffrement peut être représenté par la superposition de deux alphabets, l'alphabet clair présenté dans l'ordre normal et l'alphabet chiffré décalé à droite, du nombre de lettres voulu. Nous avons ci-dessous l'exemple avec la clé de chiffrement de 3 :

```
alphabet_in  : abcdefghijklmnopqrstuvwxyz
alphabet_out : defghijklmnopqrstuvwxyzabc
```

Pour chiffrer un message, il suffit de regarder chaque lettre du message clair, et d'écrire la lettre chiffrée correspondante. Pour déchiffrer, il suffit de faire l'inverse, soit de décaler chaque lettre du message chiffré de 3 positions vers la gauche.

```
texte clair   : "nous sommes des eleves de seconde en stage chez st"
texte chiffré : "qrxv vrpphv ghv hohyhv gh vhfrqgh hq vwdjh fkhc vw"
```

### Attaque

Il existe plusieurs attaques possibles pour casser le chiffre de César : 

* Par **force brute** : sur une portion de message chiffré, on teste tous les décalages possibles jusqu'à trouver un sens

|   Décalage (clé)      |   Texte de test |
|---                    |---        
| 0 | hohyhv gh vhfrqgh |
| 1 | fmfwft ef tfdpoef |
| 2 | gngxgu fg ugeqpfg |
| 3 | eleves de seconde |
| 4 | ipiziw hi wigsrhi |
...

* Par **analyse de fréquences** : on trie les lettres par rapport à leur fréquence d'apparition dans le texte chiffré et on les compare avec l'ordre d'apparition des lettres de la langue d'origine. Plus le texte est court, plus les lettres peuvent apparaître un même nombre de fois. Dans ce cas, il peut y avoir plusieurs possibilités de déchiffrement. Le mieux est de les explorer par force brute jusqu'à déchiffrer correctement le message.

**Exemple**

```
texte chiffré 1 : "qrxv vrpphv ghv hohyhv gh vhfrqgh hq vwdjh fkhc vw"
texte chiffré 2 : "qrxv vrpphv ghv hohyhv gh vhfrqghv hq vwdjh fkhc vw. oh vxmhw gh vwdjh sruwh vxu o'hwxgh gh od uhvlvwdqfh g'xq fkliiuhphqw vbphwultxh idfh d od fubswdqdobvh prghuqh. oh exw hvw gh wurxyhu ghv prbhqv gh ghihqvh frqwuh o'dwwdtxh sdu dqdobvh iuhtxhqwlhooh ghv ohwwuhv. qrxv doorqv wudydloohu hq elqrph, dxwrxu gh vxmhw pdwkhpdwltxhv hw lqirupdwltxh, dyhf o'rxwlo sbwkrq. fhfl hvw xq shwlw phvvdjh fodlu."
```

|   Texte chiffré      |   Fréquence d'apparition des lettres |
|---                   |---        
| 1 | h:10, v:8, q:3, r:3, g:3, p:2, f:2, w:2, o:1, y:1, x:1, d:1, j:1, k:1, c:1, {a,b,e,i,l,m,n,s,t,u,v,x,z} = 0 |
| 2 | h:64, w:31, v:30, d:24, q:20, o:19, x:18, u:18, r:15, g:14, l:13, p:11, f:11, i:6, b:6, s:5, t:5, y:4, k:4, j:3, m:2, e:2, c:1, a:0, n:0, z:0 |




