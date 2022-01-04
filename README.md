# Kolmogorov-et-detection-du-visage-
Classification de visage à l'aide basé sur la compléxité de Kolmogorov


# <span style="color:red">  Usage de la complexité de Kolmogorov pour détecter les visages similaires

#### Complexité de Kolmogorov

La théorie de l'information algorithmique repose sur un principe simple défini par Kolmogorov : la complexité de Kolmogorov d'un objet - nombre, image numérique chaîne de chactères - est la taille du plus petit algorythme (dans un certain language de programmation fixé) qui engendre cet objet.

La complexité de Kolmogorov KM(x), ou complexité algorithmique, d’une suite x finie de caractères pour une machine M est déﬁnie par :

$$
K_M(x) = \min_{p \in P_M} \{ l(p) , s(p) = x \}
$$

Dans notre cas, nous nous intérressons à la compléxité conditionnelle K(x1|x2) entre deux images.

$$
K_M(x_1|x_2) = \min_{p \in P_M}\{ l(p), s(x2,p) = x1 \}
$$

Bin que la complexité de Kolmogorov soit incalculable il a été demontré que nous pouvons raisonnablement l'approché par le nombre de bits nécessaires pour coder x à l'aide d'un compresseur C (par exemple gzip, izma ...) i.e. :

$$
K(x) \approx C(x)
$$


#### Mesure de similarité par l'approximation de la compléxité de Kolmogorov

Nous avons défini la compléxité de Kolmogorov comme la messure du contenu en information algorythmique d'un objet.
Nos pouvons l'utiliser pour estimer une mesure de similarité entre deux objets. Soit calculer la distance d'information normalisé (NID) : 

$$
NID(x,y) = \frac{\max\{K(x|y), K(y|x) \}}{\max\{K(x),K(y) \}} = \frac{K(x,y) - min(K(x), K(y))}{\max(K(x),K(y))}
$$


où, $K(x,y)$ : complexité de la concaténation de x et y.

Cependant cette métric n'est pas calculable.

---
Apparté : 

La distance d'information est absolue, mais si nous voulons exprimer la similarité, nous sommes plus intéressés par les distances relatives. Par exemple, si deux chaînes de longueur 1 000 000 diffèrent de 1000 bits, nous considérons que ces chaînes sont relativement plus similaires que deux chaînes de 1000 bits qui diffèrent de 1000 bits. Il faut donc normaliser pour obtenir une métrique de similarité. De cette façon, on obtient la distance d'information normalisée (NID).

---

Comme NID n'est toujours pas calculable, nous pouvons utiliser son approximation par compréssion, afin d'obtenir la distance de compréssion normalisé (NCD), ***réécriture de NID par Vitanyi et Cilibrasi*** :

$$
NCD(x,y) = \frac{C(x,y) - min(C(x), C(y))}{\max(C(x),C(y))}
$$

La NCD est en fait une famille de distances paramétrées par le compresseur C. Plus C est bon, plus la NCD se rapproche de la NID, et meilleurs sont les résultats. 

$C(x,y)$ est içi la taille de l'image concaténé.
