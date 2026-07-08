# Comprehension

ETU004286
ETU004175 

## Les codes qu'on a compris:

Fichier: connection.php
- Ce fichier sert de connection a la base. La fonction dbconnect() retourne la connection a la base, cette derniere se fait par le biais de la fonction integre dans php: mysqli_connect() qui permet la connection a la base

Fichier: functions.php

- function get_all_lines:
    - function mysql_query = creer la requete sql selon notre base
    - cette fonction retourne toutes les lignes d'une requete sql avec la boucle while et l'utilisation de mysqli_fetch_assoc() qui fetch et execute la requete

- function get_one_line:
    - retourne seulement une ligne (la premiere) du resultat de la requete. En effet, on appel seulement une seule fois mysql_fetch_assoc

- function get_all_departements:
    - retourne la liste des departements avec: nom departement, numero departement, manager actuel, nb employes.
    - on a une requete complexe:
        - fonction CONCAT(e.first_name, ' ', e.last_name) permet de concatener (assembler) first name avec last name avec un espace au milieu.
        - le sub-query a l interieur compte le nombre d'employe dans un departement
        - on join avec les tables autres tables necessaires. Le left join permet d'avoir null si jamais un departement n'a pas de manager ou d'employe.
        - l'order by permet de lister du plus petit au plus grand les lignes de reusltat par departement numero

function get_jobs_stats():
    - retourne les statistics par emploi:   Emploi	Hommes	Femmes	Total	Salaire moyen 
    - SUM permet de sommer par emxempe le nombre d'homme (M) et de femme (F)
    - COUNT(*) permet de compter tous les eomployes
    - AVG permet de faire une moyenne

function execute_query:
    - exectue une requete

function get_current_department($emp_no)
    - sprintf($sql, $emp_no) permet de remplacer le %s par la valeur de $emp_no

function change_departemnet:
    - update: change le departemnet d'un employe
    - insert: on insert dans dept_emp pour la table d association de departement et d'employe. Or on a compris que ON DUPLICATE KEY UPDATE  permet de ne pas insere si la ligne existe deja. on update seulemet la lignes. Nous pensons que c'est l'equivalent d'un IF ELSE

function get_current_manager():
    - retourne le manager actuel d'un departement.
    

function make_manager:
    - un employe devient manager d'un departement
    - on update le statut du departemnemt
    - on insert dans dept manager

function CRUD department, employee, manager

function get_one_department:
    - permet d'avoir dept_no et dept_name d'un department

Fichier: become_manager.php
    - include(): include le fichier dans la page pour pouvoir utiliser ces fonctionalite
    - dans cette page on a un formulaire avec http request POST qui permet de devenir manager a partir d une date de debut et qui renvoie a la meme page mais avec emp_no comme parametre. Cette requete est recu par:     if ($_SERVER['REQUEST_METHOD'] === 'POST' && $current_dept) { qui check si on a bien POST et que $current_dept est vrai c'ets a dire si la query bien ete execute. 
    - il existe 3 resutlats possible pour la condition dans le traitement du POST: 
        - si date non saisie: resaisir error
        - si date saisie mais avant la date du manager actuel: doit etre apres date manager actuel error
        - sinon: on insert. On pose success=true pour dire que l'insert a bien ete execute.
    - dans le render html, on met des checks si employe trouve, pas de departement actuel. Sinon on l'affiche. Si devenir manager a ete un succes: en vert on met un message de success, sinon on affiche l'erreur. La varibale $error a ete passe dans le code php au dessus
    - affichce manager actuel selon l'affichage: nom manager + " depuis le " + date_debut du manager. Si le manager est null, on affiche aucun

Fichier: change_dept.md
    - formulaire POST pour permetre de changer le departement d'un employe. On met en parametre le numero de l'employe
    - en code php, on a le check: nouveau departement choisi, date de debut ont ete saisie. date saise doit etre apres la date d'avant. Ensuite on change avec l'appel de la fonction de functions.php: change_department
    - meme check sucess et affichage que dans la page become_manager.php

Fichier: dept_form.php
    - permet d'ajouter ou d'update un departemnt si deja existant.
    - check de departement numero et nom, taille du numero doit etre au minimum de 4 cahracter.
    - ce formulaire change selon qu'on edit ou qu'on veut ajouter un nouveau departemnt. C'est ce que fait la variable $mode

Fichier emp_form.php:
    - meme logique que dept_form mais pur l'employe

Fichier: employees;
    - on a une foncitonanlite de pagination avec 20 elements affiche par page.
    - offset: sauter les pages

## Les codes qu'on a pas compris:
Fichier: functions.php
L'utilisation recurente de 9999-01-01

Fichier: employees.php
$page = max(1, (int)($_GET['page'] ?? 1));


## Les fonctions utilisee que vous ne connaissez pass 
Fichier: functions.php
function get_departments_except:
    - syntaxe: WHERE dept_no <> '%s' avec le <>

Fichier: become_manager.php
    - htmlspecialchars($error)

Fichier change_dept.php:
    - urlencode()

Fichier: /src-tp-real/pages/
