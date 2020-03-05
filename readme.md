# E-Commence Project

## Setup

'
mkdir templates static static/css static/js static/img
touch readme.md env.py templates/base.html
echo -e "eny.py\n*.sqlite3" >> .gitignore
sudo pip3 install django-forms-bootstrap
sudo pip3 install Pillow
sudo pip3 install stripe
'

## env.py

'
import os

os.environ["DEVELOPMENT"] = "Yes"
os.environ["HOSTNAME"] = "127.0.0.1"
os.environ["SECRET_KEY"] = "2+=6ylxler=d2&fmnhj4pp&+z)b+axy%avrtju--t&!5v=6*+)"
os.environ["DATABASE_URL"] = "postgres://txbitamqocrnlg:20f02f79d9e34004d5381243e11f0a394b5bcf249d1509814779644c77fb9331@ec2-54-246-90-10.eu-west-1.compute.amazonaws.com:5432/db1cei3144aff4"

'
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

## Start project
'django-admin startproject' --> My shortcut is 'pstart'

so you would use 'pstart ecommence .'

You may need to make the manage.py file executable

'chmod +x manage.py'

## Add sqlite3 to gitignore

This may be useless after the additions I have made above.

'
echo '*.sqlite3' >> .gitignore
'

## Copy previous Project over from 'django authentication'

Copy the 'accounts' folder over and place in this project.
Copy the 'css' folder from the 'static' folder.

## Update Settings.py

Because we have copied accounts app we need to update the settings.py

Add to INSTALLED_APPS -> 'accounts',
above the new entry add (This should been install already with 'sudo pip3 install django-forms-bootstrap')
'    
    'django_forms_bootstrap',
'
Since we have reused the accounts,

We have to add this to just below the AUTH_PASSWORD_VALIDATORS block

'
AUTHENITCATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',
    'accounts.backends.CaseInsensitive',
    'accounts.backend.EmailAuth'
]
'

we have updated the 'backends.py'

Below the STATIC SECTION

### Extra Static Section

I have added the following
'
STATICFILES_DIRS = (os.path.join(BASE_DIR, 'static'),)
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
'

add

'
MESSAGE_STORAGE = 'django.contrib.messages.storage.session.SessionStorage'
'

In the TEMPLATES block change the 'DIRS' to

'
'DIRS': [os.path.join(BASE_DIR, 'templates')],
'

This tells django that multiple templates folders contain templates.

## Sorting the urls.py (ecommence)

This is what the file should contain.

'
from django.conf.urls import url, include
from django.contrib import admin
from accounts import urls as urls_accounts

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^accounts/', include(urls_accounts)),
'


# Run the server and goto 

hostname/accounts/register

# Creating an Home App

These are pages not relating to the E-Commence App.

'astart home'

Make a templates folder and populate with index.html

'mkdir home/templates'
'touch home/templates/index.html'

## index.html

'
{% extends 'base.html' %} {% block content %} {% endblock %}
'

# Creating an Products App

Because you cannot have an eccommence site with out products.  This will house all our core logic so that we can upload it to our webpage.

'astart products'

# Creating a Cart App

'astart cart'
'touch cart/contexts.py'

The difference between Cart and Products is the contexts.py

# Updated the views.py in cart

This allows you to add a quantity to the same item.

'
def add_to_cart(request, id):
    """Add a quantity of the specified product to the cart"""
    quantity = int(request.POST.get('quantity'))

    cart = request.session.get('cart', {})
    if id in cart:
        cart[id] = int(cart[id]) + quantity      
    else:
        cart[id] = cart.get(id, quantity) 

    request.session['cart'] = cart
    return redirect(reverse('index'))
'

# Making the Cart.html

We can add items to the cart but not actually see them, so create a 'templates' folder in cart.

'
mkdir cart/templates
touch cart/templates/cart.html
'

# Make a Search App

'astart search'
'touch search/urls.py'

# Styling the App

First we need some font-awesome icons.

goto "https://fontawesome.com/how-to-use/on-the-web/setup/hosting-font-awesome-yourself"

Download the folder and unzip.

Create a folder in the 'static' folder called 'font-awesome'

'
mkdir static/font-awesome
mkdir static/font-awesome/css static/font-awesome/fonts
'

Then copy the css and fonts folder from the downloaded and unzipped file.

# Custom.css

Change our own css file.

# Install Stripe.API

'
sudo pip3 install stripe
'

Goto www.stripe.com
and setup and account if not already done so.