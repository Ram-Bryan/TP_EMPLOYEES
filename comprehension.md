# Comprehension

**ETU004286 — ETU004175**

---

## 1. Les codes qu'on a compris

### `connection.php`

Ce fichier sert de connection a la base. La fonction `dbconnect()` retourne la connection a la base, cette derniere se fait par le biais de la fonction integre dans PHP : `mysqli_connect()` qui permet la connection a la base.

---

### `functions.php`

#### `get_all_lines()`
- `mysql_query` = creer la requete SQL selon notre base.
- Cette fonction retourne toutes les lignes d'une requete SQL avec la boucle `while` et l'utilisation de `mysqli_fetch_assoc()` qui fetch et execute la requete.

#### `get_one_line()`
- Retourne seulement une ligne (la premiere) du resultat de la requete. En effet, on appelle seulement une seule fois `mysql_fetch_assoc`.

#### `get_all_departements()`
- Retourne la liste des departements avec : nom departement, numero departement, manager actuel, nb employes.
- La requete est complexe :
    - `CONCAT(e.first_name, ' ', e.last_name)` permet de concatener first name avec last name avec un espace au milieu.
    - Le sub-query a l'interieur compte le nombre d'employes dans un departement.
    - On join avec les autres tables necessaires. Le `LEFT JOIN` permet d'avoir `null` si jamais un departement n'a pas de manager ou d'employe.
    - `ORDER BY` permet de lister du plus petit au plus grand les lignes de resultat par numero de departement.

#### `get_jobs_stats()`
- Retourne les statistiques par emploi : Emploi, Hommes, Femmes, Total, Salaire moyen.
- `SUM` permet de sommer par exemple le nombre d'hommes (M) et de femmes (F).
- `COUNT(*)` permet de compter tous les employes.
- `AVG` permet de faire une moyenne.

#### `execute_query()`
- Execute une requete.

#### `get_current_department($emp_no)`
- `sprintf($sql, $emp_no)` permet de remplacer le `%s` par la valeur de `$emp_no`.

#### `change_department()`
- **Update** : change le departement d'un employe.
- **Insert** : on insere dans `dept_emp` pour la table d'association de departement et d'employe. `ON DUPLICATE KEY UPDATE` permet de ne pas inserer si la ligne existe deja — on update seulement la ligne. Nous pensons que c'est l'equivalent d'un `IF ELSE`.

#### `get_current_manager()`
- Retourne le manager actuel d'un departement.

#### `make_manager()`
- Un employe devient manager d'un departement.
- On update le statut du departement.
- On insere dans `dept_manager`.

#### CRUD department / employee / manager
- Fonctions de creation, lecture, mise a jour et suppression pour les departements, employes et managers.

#### `get_one_department()`
- Permet d'avoir `dept_no` et `dept_name` d'un departement.

---

### `employees.php`

- `get_title_history($emp_no)` : avoir le titre et la date dans la table `titles` par employe, par ordre decroissant.
- `get_salary_history($emp_no)` : avoir l'historique des salaires d'un employe, par ordre decroissant.
- `get_longest_title($emp_no)` : recupere la duree du travail dans le `title` le plus longtemps occupe.
- `get_one_employee($emp_no)` : recuperation integrale des informations d'un employe.
- `count_employees_by_department($dept_no)` : compte le nombre total d'employes par departement.
- Fonctionnalite de **pagination** avec 20 elements affiches par page. `offset` permet de sauter les pages.

---

### `become_manager.php`

- `include()` : inclut le fichier dans la page pour pouvoir utiliser ses fonctionnalites.
- Cette page contient un formulaire avec une requete HTTP `POST` qui permet de devenir manager a partir d'une date de debut, et qui renvoie a la meme page avec `emp_no` comme parametre.
- La requete est recue par : `if ($_SERVER['REQUEST_METHOD'] === 'POST' && $current_dept)` — qui verifie que la methode est bien `POST` et que `$current_dept` est vrai (c'est-a-dire que la query a bien ete executee).
- Il existe 3 resultats possibles pour le traitement du `POST` :
    - Si la date n'est pas saisie → erreur : resaisir.
    - Si la date est saisie mais avant la date du manager actuel → erreur : la date doit etre apres celle du manager actuel.
    - Sinon → on insere. On pose `success = true` pour dire que l'insert a bien ete execute.
- Dans le render HTML :
    - On verifie si l'employe est trouve, s'il n'a pas de departement actuel. Sinon on l'affiche.
    - Si devenir manager a reussi : un message de succes s'affiche en vert. Sinon on affiche l'erreur (la variable `$error` est passee dans le code PHP au-dessus).
    - Affichage du manager actuel : nom manager + `" depuis le "` + date de debut du manager. Si le manager est `null`, on affiche `"aucun"`.

---

### `change_dept.php`

- Formulaire `POST` pour permettre de changer le departement d'un employe. On passe en parametre le numero de l'employe.
- En PHP, on verifie : nouveau departement choisi, date de debut saisie, et que la date saisie soit apres la date precedente. Ensuite on appelle `change_department()` de `functions.php`.
- Meme logique de succes et d'affichage que dans `become_manager.php`.

---

### `dept_form.php`

- Permet d'ajouter ou de mettre a jour un departement si deja existant.
- Verification : numero et nom de departement, taille du numero minimum 4 caracteres.
- Le formulaire s'adapte selon qu'on est en mode edition ou creation — c'est ce que gere la variable `$mode`.

---

### `emp_form.php`

- Meme logique que `dept_form.php` mais pour l'employe.

---

### Pages PHP

- **`fiche.php`** : je comprends les boucles pour le tableau et les conditions.
- **`index.php`** : `a href` vers les pages, et liste des departements.
- **`search.php`** : on effectue les recherches via les inputs. Quand on valide, `if($submit)` affiche les resultats en bas.
- **`stats.php`** : on liste toutes les statistiques de salaires et le nombre d'employes.

---

## 2. Les codes qu'on a pas compris

### `functions.php`

- L'utilisation recurrente de `9999-01-01`.

### `employees.php`

- `$page = max(1, (int)($_GET['page'] ?? 1));`

- `search_employees($dept_no, $name, $age_min, $age_max)` : on n'a pas compris le `implode` sur le `$where`.

- `get_employees_by_department($dept_no, $limit, $offset)` : on n'a pas bien compris la demarche de l'`offset`.

### `fiche.php`

- `<?= number_format($s['salary'], 0, ',', ' ') ?>` : on ne comprend pas bien la logique des arguments `0`, `,` et `' '`.

### `search.php`

- `<?= count($results) ?> résultat(s)<?= count($results) === 200 ? ' (limité à 200)' : '' ?>` : on ne comprend pas bien la logique de ce bloc.

### `stats.php`

- `<?= number_format($row['salaire_moyen'], 0, ',', ' ') ?> €` : meme incomprehension que dans `fiche.php` pour les arguments `0`, `,` et `' '`.

---

## 3. Les fonctions utilisees qu'on ne connait pas

### `functions.php`

- `get_departments_except()` : syntaxe `WHERE dept_no <> '%s'` — on ne connait pas l'operateur `<>`.

### `become_manager.php`

- `htmlspecialchars($error)`

### `change_dept.php`

- `urlencode()`

### Autres

- `implode`
- `urlencode`
- `&larr;`