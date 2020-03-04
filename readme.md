# E-Commence Project

MyConfig
alias run="python3 manage.py runserver"
alias migrate="python3 manage.py migrate"
alias creategod="python3 manage.py createsuperuser"
alias makereq="pip3 freeze > requirements.txt"
alias pstart="django-admin startproject "
alias gignore="echo env.py > .gitignore"
alias makeenv="echo import os > env.py"
alias astart="django-admin startapp "
alias makemigrate="python3 manage.py makemigrations"

## Add sqlite3 to gitignore

'
echo '*.sqlite3' >> .gitignore
'