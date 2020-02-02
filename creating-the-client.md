# Creating the client

1. Get the Auth0 samples

```
git clone https://github.com/auth0-samples/auth0-react-samples.git
```

2. Install dependencies
```
cd auth0-react-samples/02-Calling-an-API
npm install

3. Configure Auth0 settings

Create an auth_config.json file from the auth_config.json.example.   
Then update with your Auth0 settings.  Here's mine:

```javascript
{
  "domain": "reboot2020ft.eu.auth0.com",
  "clientId": "TW7727i18TJZ6Vzbf4MJUXfrvU3pLhjx",
  "audience": "myaudience"
}
```

4. Repoint to to your API

Update ExternalApi.js line 15 to:
```javascript
const response = await fetch("http://localhost:8000/api/private", {
```

5. Run it!
```
npm start dev
```

It should be available at http://localhost:3000




