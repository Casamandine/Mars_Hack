# Web-Jonglery

## Solution

Challenge un peu plus compliqué que les autres web, il s'agit d'une attaque de type juggling à faire sur le password.

Nous mettons donc un tableau à la place de la variable "pass" :

Démonstration

Explication :

strcmp(array(), "thePassword") -> NULL

Or en php avec la comparaison faible ("==") NULL == 0 -> true

Pour contré cela on peut remplacé les "==" par "==="
