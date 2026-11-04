# Expérience : priorité des variables Ansible

## Objectif

Comprendre comment Ansible choisit une valeur lorsqu'une même variable est définie à plusieurs endroits.

## Configuration

La variable `role_serveur` peut être définie à différents niveaux :

- `group_vars/dev.yml` : variable commune au groupe DEV.
- `host_vars/yassine-vm.yml` : variable propre à l'hôte `yassine-vm`.
- `-e` : variable passée directement lors de l'exécution de la commande.

## Expérience réalisée

Dans `host_vars/yassine-vm.yml`, la variable est définie ainsi :

    role_serveur: web

Puis, le playbook est exécuté avec :

    ansible-playbook -i inventories/dev playbooks/debug-vars.yml -e "role_serveur=database"

## Résultat observé

Ansible affiche :

    Rôle du serveur : database

## Conclusion

La variable passée avec `-e` (extra-vars) prend le dessus sur les variables définies dans `host_vars` et `group_vars`.

Dans notre expérience, la valeur `database` est donc retenue à la place de `web`.