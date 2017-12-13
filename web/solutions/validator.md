# Validator

## Install

```sh
$ s add validator
```

## Usage

All validators are compliant to this repo:
[Validators](https://github.com/tamtakoe/common-validators)

```yml
endpoints:
  create-user:
    file: create_user.js
    description: Create new user
  # Endpoint can only be called from another socket( validator feature )
    public: false
    parameters:
      email:
        type: string
        description: user email
        required: true
        constraints:
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
  const {data, response, users} = Server(ctx)
  try {
    // This will return errors if args do not validate
    await socket.post('validator/validate', ctx)
    const {email: username, password} = this.props
    const profile = await users.create({username, password})
    return response.json(profile)
  } catch ({message}) {
    return response.json(message, 400)
  }
}

```
