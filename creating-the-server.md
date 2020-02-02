# Setting up the Django-based API

Note, I'm on Windoze for this, so you'll need to tweak for Mac/Linux.

1. Get the repository code
```
git clone https://github.com/andywillmot/Reboot2020.git
cd Reboot2020
```
2. Create a virtualenv (assuming you have Python 3.6+ installed) and activate it. 
```
virtualenv env
.\env\Scripts\activate.ps1 
```
The activation script you use is dependent on the shell you're using - I'm on powershell.  

3. Install the dependencies
```
pip install -r requirements.txt
```

4. Update the JWT_AUTH variable in mysite/mysite/settings.py with your Auth0 settings.  
JWT_AUDIENCE is your API identifier/audience   
JWT_ISSUER is you Auth0 domain   

5. Also update line 21 in mysite/mysite/settings.py replacing the domain name with your Auth0 one.

6. Setup the database
```
cd Reboot2020\mysite
python manage.py migrate
```
7. Run the server interactively
```
python manage.py runserver
```
8. Test
You should be able browse to http://localhost:8000/api/public and see a sucessfull JSON returned.
Also try browsing to http://localhost:8000/api/private and you should see an authentication failure provided by Django Rest Framework.




