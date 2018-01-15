# Validator

## Install

```sh
$ s add validator
```

## Usage

All validators are compliant to this repo:
[Validators](https://github.com/tamtakoe/common-validators)

```yml
name: sample
description: Description of sample
version: 0.0.1
endpoints:
  create-user:
    file: create_user.js
    description: Create new user
    public: false # Endpoint can only be called from another socket( validator feature )
    parameters:
      email:
        type: string
        description: user email
        required: true
        constraints: # Require input to match email type
          - email
      password:
        type: string
        description: User password, minimum 8 characters, max 20 characters
        required: true
        constraints:
          - minLength:
              arg: 8
          - maxLength:
              arg: 20
  ```

And create_user.js endpoint

```js
import Server from 'syncano-server'
export default async ctx => {
  const {response, users, socket} = Server(ctx)
  try {
    // This will return errors if args do not validate
    await socket.post('validator/validate', ctx)
    const {email: username, password} = this.props
    const profile = await users.create({username, password})
    return response.json(profile)
  } catch (e) {
    if(e.response) {
        return response.json(e.response.data, e.response.status)
    }
    return response.json(e.message, 400)
  }
}
```
