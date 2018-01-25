# Two factor authentication socket

- Preparation: **10 minutes**
- Requirements:
  - Initiated Syncano project
- Sockets:
  - [rest-auth](https://syncano.io/#/sockets/rest-auth)
  - [two-factor-auth](https://syncano.io/#/sockets/two-factor-auth)

### Problem to solve

You want to implement two factor authentication using Syncano Users service.

### Solution

Our solution is based on two Sockets. [rest-auth](https://syncano.io/#/sockets/rest-auth) Socket will be used for basic user registration. [two-factor-auth](https://syncano.io/#/sockets/two-factor-auth) will be used for all two factor authentication actions like setting two factor auth up and user login using two factor token.

### Setup

#### Installing server dependencies

To install `rest-auth` type:
```sh
$ syncano-cli add rest-auth
$ syncano-cli deploy rest-auth
```

To install `two-factor-auth` type:
```sh
$ syncano-cli add two-factor-auth
$ syncano-cli deploy two-factor-auth
```

#### JavScript client setup
Install

```sh
$ npm install syncano-client --save
```
or

```HTML
<script src="https://unpkg.com/syncano-client"></script>
```

Basic connection

```javascript
const s = new SyncanoClient('YOUR-INSTANCE-NAME');
```

### Actions for two factor authentication

#### Register a new user
To register a new user send a request to `rest-auth/register` endpoint with

with parameters below

`username=[string]` - user email

`password=[string]` - user password

**_Using syncano-client library_**

```javascript
s.post('rest-auth/register', { username, password })
  .then((user) => {
    console.log(user);
  })
```

**_Using HTTP clients_**
```
  https://<your_instance_name>.syncano.space/rest-auth/register/
```

#### Setup user for two factor authentication

To setup a user account for two factor authentication send a request to `two-factor-auth/setup-two-factor`

with parameters below

`username=[string]` - user email

`token=[string]` - user token

**_Using syncano-client library_**

```javascript
s.post('two-factor-auth/setup-two-factor', { username, token })
  .then((res) => {
    console.log(res);
  })
```
**_Using HTTP clients_**

```
  https://<your_instance_name>.syncano.space/two-factor-auth/setup-two-factor/
```

This will return a response that contains the otpURL and dataURL(image url) for QR code.
The `dataURL` is the image url in base64 which is expected to be used to display a Google Authenticator–compatible QR code. 

**_Sample response_**
```
{
  message: "Verify OTP",
  tempSecret: "LBGDOZBIKARWIRZI",
  otpURL: "otpauth://totp/SecretKey?secret=LB",
  dataURL: "data:image/png;base64,iVBORw0KGgoAAAANS"
}
```

Display a QR code using the `dataURL` as `src` in an image tag
```JSX
<img src=`${dataURL}`/>
```
Scan the QR code with a two-factor auth app like
[Google Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=en)


To complete the process send another request to `two-factor-auth/verify-token` with parameters

`username=[string]` - user email

`token=[string]` - user token

`two_factor_token=[string]` - One-time passcode from two factor app like [Google Authenticator](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=en)

to verify a two-factor token before enabling two-factor authentication on a user account to prevent locking user.

**_Using syncano-client library_**

```javascript
s.post('two-factor-auth/verify-token', { username, token, two_factor_token })
  .then((res) => {
    console.log(res);
  })
```
**_Using HTTP clients_**

```
  https://<your_instance_name>.syncano.space/rest-auth/two-factor-auth/verify-token/
```


#### User login
To login a user using either normal authentication and two-factor authentication send a request to `two-factor-auth/login`

with parameters below

`username=[string]` - user email

`token=[string]` - user token

`two_factor_token=[string]` - One-time-passcode(optional for user with two factor authentication not enabled on their account)

**_Using syncano-client library_**

```javascript
s.post('two-factor-auth/login', { username, token, two_factor_token })
  .then((user) => {
    console.log(user);
  })
```
**_Using HTTP clients_**

```
  https://<your_instance_name>.syncano.space/two-factor-auth/login/
```

#### To disable two factor authentication on user account

To disable two-factor authentication on user account send a request to `two-factor-auth/login`

with parameters below

`username=[string]` - user email

`token=[string]` - user token

`two_factor_token=[string]` - One-time-passcode

**_Using syncano-client library_**

```javascript
s.post('two-factor-auth/disable-two-factor', { username, token, two_factor_token })
  .then((res) => {
    console.log(res);
  })
```
**_Using HTTP clients_**

```
  https://<your_instance_name>.syncano.space/two-factor-auth/disable-two-factor/
```

### Demo web app
Demo web app [repo](https://github.com/Syncano/synacno-react-demo-two-factor-auth-socket) with two-factor-auth socket using React client library 

