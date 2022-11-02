# lern-react
lerning react

## Step 1: Create the Project

```
npx create-react-app react-jwt-auth
```

- Router to implement pages, we will use react-router for this,
- Login page which we will get user information and send login request to set JWT token
- Home page which just be accessible for authenticated users.

```
yarn add react-router-dom
npm install react-router-dom
```

### add folder 

react-jwt-auth\src\helpers\history.js

```
import { createBrowserHistory } from 'history';
 
export const history = createBrowserHistory();
```


### src\routes.js

```
import React from "react";
import { Redirect, Switch, Route, Router } from "react-router-dom";
import RouteGuard from './components/RouteGuard';

//history
import { history } from './helpers/history';

//pages
import HomePage from "./pages/HomePage"
import LoginPage from "./pages/Login"

function Routes() {
    return (
        <Router history={history}>
            <Switch>
                <Route exact path="/" component={HomePage} />
                <Route path="/login" component={LoginPage} />
                <Redirect to="/" />
            </Switch>
        </Router>
    );
}

export default Routes
```


### Updating App.js

react-jwt-auth\src\App.js

```
import './routes';
```

## Step 2: Creating RouteGuard Component

### react-jwt-auth\src\components\RouteGuard.js
```
import React from 'react';
import { Route, Redirect } from 'react-router-dom';

const RouteGuard = ({ component: Component, ...rest }) => {
    function hasJWT() {
        let flag = false;
        //check user has JWT token
        localStorage.getItem("token") ? flag = true : flag = false
        return flag
    }

    return (
        <Route {...rest}
            render={props => (
                hasJWT() ?
                    <Component {...props} />
                    :
                    <Redirect to={{ pathname: '/login' }} />
            )}
        />
    );
};

export default RouteGuard;
```

## Step 3: Creating Home and Login Page

react-jwt-auth\src\pages\Home.js

```
function HomePage() {
   return (
     <div>
         Home Page
     </div>
   );
 }
  export default HomePage;
```






```
yarn add axios history -s

```
