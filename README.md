# Ansible Test

Ce dépôt contient les fichiers de configuration et les playbooks Ansible pour la gestion et le test des machines virtuelles avec Vagrant.

## Structure du dépôt


├── cmd.md # Fichier contenant des exemples de commandes pour les playbooks

├── docker_key # Clé privée SSH pour l'accès aux conteneurs Docker

├── docker_key.pub # Clé publique SSH pour l'accès aux conteneurs Docker

├── inventory_docker.ini # Inventaire Ansible pour les conteneurs Docker

├── inventory_vagrant.ini # Inventaire Ansible pour les machines virtuelles Vagrant

├── playbooks # Dossier contenant les playbooks Ansible

└── Vagrantfile # Fichier de configuration Vagrant pour créer des machines virtuelles de test