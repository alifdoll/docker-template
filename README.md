# Docker Configuration

This repository contains file that will help you start your docker
container.
So you just need to create the container, and start doing your project

## Configurations For

1. Laravel Project
2. Mysql and Phpmyadmin
3. PostgreSQL and pgadmin
4. Nodejs project

## For Permission On Root Folder

# give your current user rwX permissions recursively

sudo setfacl -Rm u:$(whoami):rwX .

# ensure new files automatically inherit those ACLs

sudo setfacl -dRm u:$(whoami):rwX .
