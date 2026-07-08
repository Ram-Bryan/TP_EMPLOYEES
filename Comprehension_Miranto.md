**Code que j ' ai compris***
    - la fonction get_title_history($emp_no) : avoir title et date dans la table titles par employe par ordre decroissante 
    - function get_salary_history($emp_no) : avoir les salaire historique d ' un employe qui se termine par ordre decroissante 
    - function  get_longest_title($emp_no) : recupere dureee du travail dans un titles le plus longtemps 
    - function get_one_employee($emp_no) : recuperation integrale de l 'infromation d 'un emplyes 
    -count_employees_by_department($dept_no) : compte le nbre total d 'emplyoes par departement 

    -page fiche.php : je comprend les boucle pour le tableau et les condition
    -page index.php :  a href vers les pages , et lister les departements 
    -page serch.php : on faits les recherche via les inputs et quand on valide la recherche if($submit) on affiche les resultats en bas 
    -page stats.php : on listes tous les statistiques de salires et les nombre des employes 
    
**Code que j ' ai pas compris**
    - function search_employees($dept_no, $name, $age_min, $age_max) : j 'ai pas compris le implode sur le $where 
    - function get_employees_by_department($dept_no, $limit, $offset) : j 'ai pas bien compris la demarche du ofset 

    -page fiche.php : Historique des salaires : <td><?= number_format($s['salary'], 0, ',', ' ') ?>  je comprend pas bien cette logique , de 0 , virgule , ' ' 
    - page search.php : comprend pas bien la logique du compte <?= count($results) ?> résultat(s)<?= count($results) === 200 ? ' (limité à 200)' : '' ?></h2>  , 
    -page stats.php : je comprend pas la logique du code <td><?= number_format($row['salaire_moyen'], 0, ',', ' ') ?> €</td> les , 0 , virgule et ' '

**fonctions utilisées que vous ne connaissez pas** : implode , urlcode ,&larr , number_format