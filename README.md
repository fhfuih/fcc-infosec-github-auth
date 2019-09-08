**FreeCodeCamp**

## `.env` entries

```
SESSION_SECRET=
DATABASE=
GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
```

## Things not mentioned: `.env`
Add `dotenv` package to import `.env` variables. See its docs for mor info.

## Things not mentioned: updating packages

The MongoDB in the boilerplate is quite outdated. After updating to `^3.0`, the connection codes should be 

```js
mongo.connect(process.env.DATABASE, { useNewUrlParser: true, useUnifiedTopology: true }, (err, client) => {
    if(err) {
        console.log('Database error: ' + err);
    } else {
        const db = client.db('infoSec');
        console.log('Successful database connection');
        // use this db below
```

## Things not mentioned: fields/schema of `profile` in `GithubStrategy` constructor

In my case, the `email` field is void. So one may add some simple `null` checker.
```
{$setOnInsert:{
    // ...
    photo: (profile.photos && profile.photos[0]) ? (profile.photos[0].value || '') : '',
    email: (profile.emails && profile.emails[0]) ? (profile.emails[0].value || 'No public email') : 'No public email',
```

## Questions

~~Why `req.isAuthenticated()` survives redirect (i.e. returns the correct value in `/profile` when redirected from another route `/auth/github/callback`), 
but cannot survive using local strategy in the last challenge?~~ session is not used in this challenge
