# Mars@Hack

## Challenge Web_Jonglery


### Intitulé du challenge :
Trouver un moyen de se connecter à l'interface de ce site.
<FONT COLOR="#ff0000">Accès au site :<br>   <a href="http://game2.marshack.fr:8087" target="new">http://game2.marshack.fr:8087</a></FONT> <p>

Nous mettons donc un tableau à la place de la variable "pass" :

Démonstration

Explication :

strcmp(array(), "thePassword") -> NULL

Or en php avec la comparaison faible ("==") NULL == 0 -> true

Pour contré cela on peut remplacé les "==" par "==="
