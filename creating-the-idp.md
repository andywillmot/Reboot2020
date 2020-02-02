# Setting up Auth0

1. Got to Auth0.com and sign up
2. Follow the wizard and create a tenant and a personal account
3. When you're on the *Getting Started* page, go to Applications on the left menu and create a new app (or edit the default one)
4. Update your Callback URLs to:
```
http://localhost:3000
```
Ok, it's not https - so not particularly secure as any man in the middle could read the tokens - but this is just a test!  

5. I also updated Allowed Web Origins to the same. Not sure how important this one is, but I did have to setup CORS on the API server to get this to work.
6. Save the changes and go to API menu
7. Create a new API.  Enter a name and an audience (this is used as config within the django API and react client).  Leave everything else as defaults and save.
8. Lastly, click on Users and Roles menu to create a user that you'll use to login to the react app with.

That should be it!.  You now have 21 days free trial to play with your IDP.


