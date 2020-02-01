# Creating the react OIDC client

1) Create the base react app (assuming you already have node.js installed)
```
npx create-react-app client
```

2) Install the dependencies
```
npm install --save react-openidconnect
```

2) Change app.js to

```javascript
import React, { Component } from 'react';
import Authenticate from 'react-openidconnect';
import OidcSettings from './oidcsettings';
 
class App extends Component {
 
  constructor(props) {
    super(props);
    this.userLoaded = this.userLoaded.bind(this); 
    this.userUnLoaded = this.userUnLoaded.bind(this);
 
    this.state = { user: undefined };
  }  
 
  userLoaded(user) {
    if (user)
      this.setState({ "user": user });
  } 
  
  userUnLoaded() {
    this.setState({ "user": undefined });
  } 
 
  NotAuthenticated() {
    return <div>You are not authenticated, please click here to authenticate.</div>;
  }
 
  render() {
      return (
        <Authenticate OidcSettings={OidcSettings} userLoaded={this.userLoaded} userunLoaded={this.userUnLoaded} renderNotAuthenticated={this.NotAuthenticated}>
            <div>If you see this you are authenticated.</div>
        </Authenticate>
      )
  }
}
 
export default App;
```

3) Create an oidcsettings.js file in the same directory as you app.js.  Update authority and client id to the settings of your Auth0 app
```javascript
var OidcSettings = {    
    authority: 'http://reboot2020ft.eu.auth0.com',
    client_id: 'PpX3Wes7NrdM5eZx65ZymHAIzpFo6L4Z',
    redirect_uri: 'http://localhost:3000/',    
    response_type: 'code',
    scope: 'openid profile',
    post_logout_redirect_uri: 'http://localhost:3000/'      
};
```

### Sources
https://www.npmjs.com/package/react-openidconnect
