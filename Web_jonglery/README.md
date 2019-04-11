# Mars@Hack

## Challenge Web_Jonglery


### Intitulé du challenge :
Trouver un moyen de se connecter à l'interface de ce site.

![Screenshot_1](https://raw.githubusercontent.com/Casamandine/Mars_Hack/master/Web_jonglery/screenshot/Screenshot_1.png)


<FONT COLOR="#ff0000">Accès au site :<br>   <a href="http://game2.marshack.fr:8087" target="new">http://game2.marshack.fr:8087</a></FONT> <p>

### Solution :

Challenge un peu plus compliqué que les autres web, il s'agit d'une attaque de type juggling à faire sur le password.

#### Explication :

Comment à t'on su qu'il fallait faire une attaque de type juggling ?

On s'est fié à un mot qui revener souvent dans la page 'Jongleur', on l'a traduit en anglais et ça a donner 'Junggler' d'ou le nom 'juggling'.

En cherchant un peu, on est tomber sur ce <a href="https://www.owasp.org/images/6/6b/PHPMagicTricks-TypeJuggling.pdf" traget="new">diaporama</a> qui nous explique les grandes ligne de cette attaque.

En PHP, il existe **2 type de comparaison**, la comparaison dite **"Faible"** (**_Loose_** en anglais) et la comparaison **"Stricte"** (**_strict_** en anglais). Le principe est simple, en admettant qu'on utilise ce code :

```php
if (strcmp($_POST['password'], 'thePassword') == 0) {
  echo "the Flag !";
}
```

Au lieu d'envoyer un requête avec une chaîne de caractère :

```
password=toto12345
```

On envoie un tableau :

```
passsword[]=
```

PHP traduit les variables POST comme celle-ci en un tableau vide, ce qui force strcmp() à donner un null :

```
strcmp(array(), "thePassword") -> NULL
```

Or si on se rappelle bien dans notre fonction en php :

```php
if (strcmp($_POST['password'], 'thePassword') == 0) { // comparaison Faible "=="
  echo "the Flag !";
}
```

avec la comparaison faible ("==") **NULL == 0 !** Donc authentification bypass !

#### Démonstration :

Poue ce challenge, on a utilisé OWASP **Z**ed **A**ttack **P**roxy (**ZAP**) pour pouvoir modifié la variable envoyer.

![Screenshot_2](https://raw.githubusercontent.com/Casamandine/Mars_Hack/master/Web_jonglery/screenshot/Screenshot_2.png)

On met donc un tableau à la place de la variable "pass" :

![Screenshot_3](https://raw.githubusercontent.com/Casamandine/Mars_Hack/master/Web_jonglery/screenshot/Screenshot_3.png)

Puis on envoie la requête et on peut apercevoir le flag s'afficher sur le site.

![Screenshot_4](https://raw.githubusercontent.com/Casamandine/Mars_Hack/master/Web_jonglery/screenshot/Screenshot_4.png)

Ainsi le flag était :

```
MARS{TyP3JuGliNgC00LT00}
```

#### Pour contré cela :

Pour contré cela on peut remplacé les "==" par "===", donc utilisé la comparaison **"Stricte"**.

Mais aussi on peut utilisé des fonctions comme `password_hash()` et `password_verify()`.

De plus, il vaut mieux stocker les mots de passe dans un base de donnée et eviter de l'écrire en brute dans application. 
