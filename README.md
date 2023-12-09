<!-- """ 
@author : Shubham Rajput  

**Login System in Python using Django lib *** -->

>>>>     pip install virtualenv

<!-- we will create a virtual environment for our project to work on -->

>>>>     virtualenv loginsystem

<!-- change directory to  -->

>>>>     cd .\loginsystem\ 

<!-- activate the environment -->

>>>>     scripts/activate

<!-- install django in the virtual environment -->

>>>>     pip install django==4.2.7

<!-- create a project called login -->

>>>>     django-admin startproject login

<!-- create an application inside loginsystem -->

>>>>     python manage.py startapp authentication


<!-- urls.py inside login -->

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('authentication.urls'))
]

<!-- create urls.py inside authentication -->
<!-- add the code given below -->
from django.contrib import admin
from django.urls import path, include
from . import views

urlpatterns = [
    path('', views.home, name="home")
]

<!-- go to views.py inside authentication -->

from django.shortcuts import render
from django.http import HttpResponse

#Create your views here.
def home(request):
    return HttpResponse("Hello i am working")

<!-- run the server -->

>>>>     python manage.py runserver

How does this django app works
when we deploy a django website or even run it on a local host
1. django first searches for a python file called "settings.py"
2. then it will check for what all settings are you using for this app, so that this app will run accordingly
3. then it will check urls of the project, now in login's urls.py we have included the url for the app authentication
4. in the authentication's url it will go and again search for the url, and according to that url it will run the functions mentioned ( views.home )inside the url.
5. our function "home" which was written in url path of authentication app will return an HttpResponse which says "Hello i am working".
6. after which you run the server using python manage.py and a url appears in terminal
7. that's how a django app works

if we are using models or databases over here django will again go to models.py in the app
then returns a response accordingly to your views and then your views may return an http response or an html template


"""

now i will create views for signup, signin, and signout for my login system
therefore i will give url path for each function

and then create functions in views.py of authentication app
return render()
for now i will return an html template inside these functions
Return an HttpResponse whose content is filled with the result of calling django.template.loader.render_to_string() with the passed arguments.

>    def signup(request):
>        return render(request, "authentication/signup.html")

>    def signin(request):
>        return render(request, "authentication/signin.html")
    
>    def signout(request):
>        pass

the next thing is to create html template for the app
for which we will create a folder called templates in the project under loginsystem
under templates i will create another folder called authentication
and inside that folder i will create a new file say index.html
another file say singup.html
another file say signin.html

inside home function we can return render index.html from authentication


now we will get templates for our app, in-order to save time i will not focus on the front end
i will just make use of html5-boilerplate

why do i use html5-boilerplate? 
HTML5 Boilerplate is a professional front-end template used for setting up projects, 
creating fast and adaptable sites with little effort and set of HTML5 ready features and elements.

in index.html
over here i will type "Authentication" inside <title></title>
 <h1>Welcome to DBDA SMVITA</h1>
 <h2>Create a new account</h2>
 <h3>it's quick and easy</h3>

here h1,h2,h3 has different purpose as to how the title should look like and h1 being the biggest title size for all.

and empty the body section of html

in body we will display our heading <h3>"Welcome to DBDA SMVITA</h3>
after which i would like to have a button so that when the user clicks on the button, he/she will be redirected to signup,signin,signout page

<button type="submit">Sign-up</button>
<button type="submit">Sign-In</button>
<button type="submit">SignOut</button>

now we will have to tell django what is the directory for this button
so we will go into settings.py, we will search for templates and here in the directories 
'DIRS': ["templates"]

we will run the server and visit the website

here the buttons dont have functionality yet
so we will give these buttons their urls for the functions written for them

we will go to index.html
here we will give an anchor tag for the urls
<button type="submit"> <a href="/signup"></a>Sign-up</button>
<button type="submit"> <a href="/signin"> Sign-In</a></button>
<button type="submit"> <a href="/signout"> SignOut</a></button>

what is the function for signup doin, it is basically render a signup.html template

so here you will again use html5-boilerplate
and remove the body and add:
        <h3>Sign-up</h3>

so this is working, now we will create a form so the user when fills the form
will be able to register

<label for="">Username</label>
<input type="text" id="username" name="username" placeholder="Create a username (only letters and numbers)" Required> 

use this code above for first name, last name,email, password, confirm password

<form action="">
        {% csrf_token %}

            <label for="">Username</label>
            <input type="text" id="username" name="username" placeholder="Create a username (only letters and numbers)" Required> 
        
            <label for="">First Name</label>
            <input type="text" id="fname" name="fname" placeholder="Enter your First Name" Required> 

            <label for="">Last Name</label>
            <input type="text" id="lname" name="lname" placeholder="Enter your Last Name" Required> 

            <label for="">Email Address</label>
            <input type="email" id="email" name="email" placeholder="Enter your Email Address" Required> 

            <label for="">Password</label>
            <input type="password" id="pass1" name="pass1" placeholder="Enter your password" Required> 

            <label for="">Confirm your Password</label>
            <input type="password" id="pass2" name="pass2" placeholder="Confirm your password" Required> 
        </form>

type as password will give asterisks or dot and type email will take email type

whenever we create a form in django app, always use a csrf_token

now for our form we are going to have a button of type submit

what kind of method is our form using, which will be "post" method,
when we submit our form what action will this form take, so for this action
we'll just route this url to signup

since here the lines wont have spaces so then we will have to add <br> tags just to add spaces

<br><br> will add two spaces and in html it written side by side will function the same as-
<br>
<br>
so there is no convention to write this way

so this is how our form will look like without CSS
you can make some asthetic changes using <br> for newlines
<center></center> for making the body in center


so in signup button there's no action visible it will just refresh the page 
there we will need to give some implementations inside the signup function in views.py of our authentication app

so now we will write inside

    if request.method == "POST":

so we will take all fields entered by the user and store it in a variable so that we can play with them and work with them in the back-end.
so how will we take field from our user
for which we will use request.POST.get('') or request.POST[''] to get the input field from the input tab in signup.html and store it in a variable.

the variable name should be same as id in the input tab for our convenience.

username = request.POST['username']
fname = request.POST['fname']
lname = request.POST['lname']
email = request.POST['email']
pass1= request.POST['pass1']
pass2= request.POST['pass2']

after the user has filled the form we will register the user in a backend that is our database.
so we will make use of a django builtin library
and we will use
from it as django.contrib.auth.models import User

here we create a user object let's say we can name it as myuser = User.

here User is a model which we have imported from contrib.auth models of django

myuser = User.objects.create(username, email, pass1)
myuser.first_name = fname
myuser.last_name = lname

now we will save this user in the database

myuser.save()

when the user is registered successfully we shall show him/her a message that yes you are registered successfully 
and for this we will use messages a library of django

as soon as the user is registered he/she will get this message-
success is a function of messages which is being requested to show a typed message-
messages.success(request, "Your Account has been Successfully Created !!!")

after successfull registeration he/she should be redirected to the login page.
inside if statement
    return redirect('signin')

    redirect is a function imported from django.shortcuts which will automatically redirect to login page.

if the website is checked then it will show an error
here create_user() was suppose to be written in object creation

it is still showing an error because we have not migrated the changes
so press CTRL+C and type in terminal
>> python manage.py makemigrations

no changes detected

>> python manage.py migrate

it will migrate the changes

again run the server

>> python manage.py runserver

now write some code for signin, when the user will signin it will login the user
so go to views.py in authentication to write the code
>> if request.method == 'POST':
        username = request.POST['username']
        pass1 = request.POST['pass1']

next thing we will do is authenticate this user
we will create an object for this user and create a variable

>> user = authenticate() 
authenticate() is an inbuilt function
so django will authenticate this user and then check whether the password entered by this user matches as that of the database or not.

>> user = authenticate(username=username, password=pass1)

and then we will check if the user is not None
it may either return a None response or a not None response
it will return a None response if the user is not authenticated
it will return a not None response if the user is authenticated
if the user has given us the right credentials then we will login that user in our database

>> if user is not None:
            login(request, user)

login is a function from django.contrib.auth

if credentials are not authenticated
>>      else:
            messages.error(request, "Bad Credentials!")
            return redirect('home')


>> this will make us move to home page if credentials match     
if user is not None:
            login(request, user)
            fname = user.first_name
            return render(request, "authentication/index.html", {'fname': fname})
        else:
            messages.error(request, "Bad Credentials!")
            return redirect('home')

so here no messages appear therefore we need to make changes in the index.html file
{% for message in messages }
<div class="alert alert-{{ message.tags }} alert-dismissible fade show" role="alert">
<strong>Message:</strong>{{ message }}
<button type="button" class="close" data-dismiss="alert" aria-label="Close">
<span aria-hidden="true">&times;</span>
</button>
</div>


{% if user.is_authenticated %}
<h3>Hello {{ fname }}</h3>
<h4>You're successfully logged in.</h4>

what if the user is not authenticated then we will have to show the not authenticated message

{% else %}
<h2>Create a new student account</h2>
<br><br>
<h3>it's quick and easy</h3>
<button type="submit"> <a href="/signup"> Sign-up</a></button>
<br><br>
<h4>Already have an account?</h4>
<br><br>
<button type="submit"> <a href="/signin"> Sign-In</a></button>
{% endif %}


so after the user has been authenticated we see there's no function to signout
so we will have to give some implementation to signout function

logout(request)
messages.success(reuqest, "Logged Out Successfully!")
return redirect('home')

so our user will register itself to our website where he/she can login and logout of our system.

Now we will implement the email functionality in the app itself
so now we will need an email account itself for now let's make use of a gmail service so what we will do is create gmail account for our app

now in login dir we will create a new file called info.py
which will contain the information about our gmail account

EMAIL_USE_TLS = True
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_HOST_USER = 'emailaddress'
EMAIL_HOST_PASSWORD = 'password'
EMAIL_PORT = 587  #port for email

now we will go to settings.py
type 
from . info import *

now we give the setting of our email
EMAIL_USE_TLS = EMAIL_USE_TLS
EMAIL_HOST = EMAIL_HOST 
EMAIL_HOST_USER = EMAIL_HOST_USER
EMAIL_PASSWORD = EMAIL_PASSWORD
EMAIL_PORT = EMAIL_PORT

now in views.py of our app authentication

we will write a function which will send email to the users who successfully login in to our system
but before that we will need to do some validation if the user already exists in our database then the user wont be able to create an account with the same email.
for which we will type

        if User.objects.filter(username = username):
            messages.error(request, "Username already exists! Please try some other username.")
            return redirect('signup')

        if User.objects.filter(email = email):
            messages.error(request, "Email already registered!")
            return redirect('signup')
        
        if len(username)>10:
            messages.error(request, "Username must be under 10 characters")
            return redirect('signup')

        if pass1 != pass2:
            messages.error(request, "Passwords didn't match!")
            return redirect('signup')

        if not username.isalnum():
            messages.error(request, "Username must be Alpha-Numeric!")
            return redirect('signup')
        
now we will write some code for sending emails

from login import settings


        # Welcome Email

        subject = "Welcome to DBDA SMVITA"
        message = "Hello " + myuser.first_name + "!! \n" + "Welcome to SMVITA!! \n Thank you for visting our website \n we have sent you this confirmation email, please confirm your email address in order to activate your account. \n\n Thanking you \n Shubham Rajput \n PRN- 040"
        from_email = settings.EMAIL_HOST_USER
        to_list = [myuser.email]
        send_mail(subject, message, from_email, to_list, fail_silently = True)

here fail_silently will not let our application crash, meaning even if the email fails to send then it will not crash the app
for send_email we will import it

from django.core.mail import send_mail

Now we want to add a unique link inside our email
how can we do that?
we can make use of a library called six 

>> pip install six

now i will create a new file in my app authentication 
as tokens.py which will create string for us

from django.contrib.auth.token import PasswordResetTokenGenerator

from six import text_type

class TokenGenerator(PasswordResetTokenGenerator):
    def _make_hash_value(self, user, timestamp):
        return (
            text_type(user.pk) + text_type(timestamp)
        )

generate_token = TokenGenerator()

the user's account will be activated only if the user clicks on this unique link
from django.core.mail import EmailMessage, send_mail
from django.contrib.sites.shortcuts import get_current_site
from django.template.loader import render_to_string
from django.utils.http import urlsafe_base64_encode
from django.utils.encoding import force_bytes, force_text
from . tokens import generate_token

# Email Address Confirmation Email

        current_site = get_current_site(request)
        email_subject = "Confirm your email @ dbda - Django Login!!"
        message2 = render_to_string('email_confirmation.html',{
            'name': myuser.first_name,
            'domain': current_site.domain,
            'uid': urlsafe_based64_encode(force_bytes(myuser.pk)),
            'token': generate_token.make_token(myuser)
        })
        email = EmailMessage(
            email_subject,
            message2,
            settings.EMAIL_HOST_USER,
            [myuser.email],
        )
        email.fail_silently = True
        email.send()

now go to email_confirmation.html

write this code

{% autoescape off %}

Welcome to Django Login

Hello  {{ name }}!

Please confirm your email by clicking on the following link.

Confirmation Link: http://{{ domain}}{% url 'activate' uid64=uid token=token %}

{% endautoescape %}

now open urls.py of authentication app

 path('activate/<uidb64>/<token>', views.activate, name="activate")

 now i will have to create a new function called activate in views.py
from django.utils.encoding import force_bytes
from . tokens import generate_token

 def activate(request, uidb64, token):
    try:
        uid = force_bytes(urlsafe_base64_decode(uidb64))
        myuser = User.objects.get(pk=uid)
    except (TypeError, ValueError, OverflowError, User.DoesNotExist):
        myuser = None

    if myuser is not None and generate_token.check_token(myuser, token):
        myuser.is_activate = True
        myuser.save()
        login(request, myuser)
        return redirect('home')
    else:
        return render(request, 'activation_failed.html')
        
create activation_failed.html in root template

add these codes
{% autoescape off %}
Activation failed, please try again!
{% endautoescape %}

now create a superuser to access django admin site

>> python manage.py createsuperuser

Password (again):
Superuser created successfully.

pk is primary key