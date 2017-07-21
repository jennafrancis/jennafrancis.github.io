---
layout: post
title:  "A REACTion to Beer as a Craft"
date:   2017-07-21 04:51:22 +0000
---


FACT: There are almost five times as many breweries in the U.S. today than there were ten years ago. That's over 5,300 breweries. Don't believe me? [Check it out](https://www.brewersassociation.org/statistics/number-of-breweries/). 

Now, taking into account that most brewing companies are very small and others have multiple locations, let's cut that number back to 3,500. Let's say each company produces 3-4 different custom products. We're easily up to 10,000 beers being made... in the U.S. only.

Well I love beer, but I don't want to sort through 10,000 to find my true loves, the hoppiest of IPAs. 

**Enter: TopHop**

*"At TopHop, we know that life is better when you're hoppy.  That's why we religiously taste new releases from our favoritie breweries and report back to you with only the best." - Jenna Francis, Founder and CTO*

Yeah, that's me! The CTO of a totally made up company whose web application has been a ton of fun to make with React and Redux. 

**Rails API**

First, I set up a Rails API, using `$ rails new my_api --api` to create a lighter framework than the usual `$rails new my_app` command. Added a few models and went straight into the controller to start creating actionable routes. My controllers needed to do 4 basic things. Send all beers to the front end, create beers from inputs given on the front end, destroy beers with an id sent from the front end, and return a JWT (JSON Web Token) when a valid user logs in. The first three were fairly simple to write out with normal Rails CRUD actions rendering JSON responses. The last took a separate Auth module and a JWT encoding function with an app secret and algorithm ([more here](https://jwt.io/introduction/)).

**React / Redux**

Now came the hard(er) part. I began structuring out a React framework with a few stateless components linked back to one big App.js file. As the state became too large to manage reasonably (all those beers!), I turned to Redux. Using BrowserRouter, Route, Switch, NavLink, and Redirect from 'react-router-dom', I was able to make my app dynamically respond to changes in route. A few mapStateToProps calls and connected components later, I turned to my actions and reducers. My actions called to the API through `fetch()` and dispatched to the reducers with the responses. The most complex action I created was for user login. 

```
export default function login(creds, router) {
  let config = {
    method: 'POST',
    body: JSON.stringify({
      user: creds
    }),
    headers: {
      'Accept' : 'application/json',
      'Content-Type': 'application/json'
    }
  }

  return dispatch => {
    dispatch(authenticationRequest(creds))
    return fetch(`${API_URL}/auth`, config)
      .then(response => response.json())
      .then(body => {
        if (body.user.id) {
          localStorage.setItem('tophop.token', body.token);
          dispatch(setCurrentUser(body.user));
          router.replace(`/`)
        } else {
          dispatch(loginError(body.error))
          return Promise.reject(body)
        }
    }).catch(err => console.log("Error: ", err))
  }
}
```

First, this action sets `config` as the request to be sent to the API. User credentials are placed within a `user: {}` object and stringified to send through a POST method. The action returns with a dispatch to `'AUTHENTICATION_REQUEST'` in the reducer and then fetches to the Rails API. When it recieves the response, it checks if there is an attribute for user id. If there is, the function sets the JWT token from the Rails server into the local storage and sets a current user before redirecting to the home page. If the body does not include a user, but instead an error, the form state returns to empty strings and the form remains.  The dispatch to  `'AUTHENTICATION_REQUEST'` is shown below.

```
function authenticationRequest(creds) {
  return {
    type: 'AUTHENTICATION_REQUEST',
    isAuthenticating: true,
    isAuthenticated: false,
    creds
  }
}```

To get a full picture, I will show my Login component. You can see where I import the login action and pass it to the 'react-redux' connect function. This action is called in `handleOnSubmit` when the submit button is pressed.

```
import React, { Component } from 'react';
import { connect } from 'react-redux';
import login from '../../redux/actions/auth'

class LoginForm extends Component {
  constructor(props) {
    super(props)

    this.state = {
      email: '',
      password: ''
    }
  }

  handleOnChange = event => {
    const { name, value } = event.target;
    this.setState({
      [name]: value
    })
  }

  handleOnSubmit = event => {
    event.preventDefault();
    this.props.login(this.state, this.props.history);
    this.setState({
      email: '',
      password: ''
    })
  }

  render() {
    return (
      <div>
        <h2>Welcome back! Sign in to continue.</h2>
        <form>
          <div>
            <label>Email:</label><br />
            <input name="email" type="email" value={this.state.email} onChange={this.handleOnChange}/>
          </div>
          <br></br>
          <div>
            <label>Password:</label><br />
            <input name="password" type="password" value={this.state.password} onChange={this.handleOnChange} />
          </div>
          <br></br>
          <button onClick={this.handleOnSubmit}>Log in</button>
        </form>
      </div>
    )
  }
}

export default connect(null, { login })(LoginForm)
```

This was only one of a few different actions, but you begin to see how the redux pattern falls into your react app quite nicely.

**TopHop Demo**

Unfortunately I was in a bit of a crunch finishing up and did not get to deploy to Heroku (API) and Amazon AWS (Client), but I will attempt to do so in the next week. 

**Cheers! Final project complete!**
