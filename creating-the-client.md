# Creating the client

1. Get the Auth0 samples

```
git clone https://github.com/auth0-samples/auth0-react-samples.git
```

2. Install dependencies
```
cd auth0-react-samplesS\Sample-01
npm install
```
3. Configure Auth0 settings

Create an auth_config.json file from the auth_config.json.example.   
Then update it with your Auth0 settings.  Here's mine:

```javascript
{
  "domain": "reboot2020ft.eu.auth0.com",
  "clientId": "TW7727i18TJZ6Vzbf4MJUXfrvU3pLhjx",
  "audience": "myaudience"
}
```

4. Repoint the backend of the client to you Django API by updating src/utils/views/ExternalApi.js line 61:
From
```javascript
      const response = await fetch(`${apiOrigin}/api/external`, {
```
to
```javascript
      const response = await fetch(`http://localhost:8000/api/private`, {
```

5. Run it!  It should be available at http://localhost:3000
```
npm start dev
```






