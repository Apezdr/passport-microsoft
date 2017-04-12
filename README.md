# Passport-microsoft

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [Microsoft Graph](https://graph.microsoft.io/) using the OAuth 2.0 API.

This module lets you authenticate using Microsoft, in your Node.js applications.  
By plugging into Passport, Microsoft
authentication can be easily and unobtrusively integrated into any application or
framework that supports [Connect](http://www.senchalabs.org/connect/)-style
middleware, including [Express](http://expressjs.com/).

## Install

    $ npm install passport-microsoft

## Usage

#### Configure Strategy

The microsoft authentication strategy authenticates users using a microsoft account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

The consumer key and secret are obtained by [creating an application](https://apps.dev.microsoft.com/#/appList) at
Microsoft's developer site.

```js
    var MicrosoftStrategy = require('passport-microsoft').Strategy;
    passport.use(new MicrosoftStrategy({
        clientID: 'applicationidfrommicrosoft',
        clientSecret: 'applicationsecretfrommicrosoft',
        callbackURL: "http://localhost:3000/auth/onedrive/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ userId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'microsoft'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

```js
    app.get('/auth/microsoft',
      passport.authenticate('microsoft'));

    app.get('/auth/microsoft/callback', 
      passport.authenticate('microsoft', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });
```

## Examples

For a complete, working example, refer to the [login example](https://github.com/seanfisher/passport-microsoft/tree/master/example/login).

## Credits

  - [Sean Fisher](https://seafish.io)
  - [Sluggy Bear](http://github.com/slugbay) - Original [Microsoft OneDrive](https://github.com/slugbay/passport-onedrive) strategy, upon which this is based

  Copyright (c) 2016 Sean Fisher <[https://seafish.io](https://seafish.io)>

## Thanks

  - [Jared Hanson](http://github.com/jaredhanson)

## License

  - [The MIT License](http://opensource.org/licenses/MIT)
