
## Documentação da API

#### Envia um código por e-mail para válidação

```http
  POST /send_email
```

| Body   | Tipo       | Descrição                           |
| :---------- | :--------- | :---------------------------------- |
| `email` | `string` | **Obrigatório**. E-mail que receberá o código de verificação. |

#### Retorna 2 possíveis respostas:

status(200): 
```json
{ 
  "message": "We sent a confirmation code to your email!"
}
```
<br/>

status(400): 
```json
{ 
  "message": "Enter an existing email!"
}
```

#

#### Confirma a existencia do código no database

```http
  POST /check_email
```

| Body  | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `email`      | `string` | **Obrigatório**. E-mail que recebeu o código. |
| `codigo`      | `number` | **Obrigatório**. Código recebido pelo e-mail. |

#### Retorna 5 possíveis respostas:

status(400): 
```json
{
  "message": "Invalid or expired code!"
}
```
<br/>

status(202): 
```json
{
  "message": "Continue with customer registration"
}
```
<br/>

status(403): 
```json
{
    "_id": "string",
    "name": "string",
    "lastName": "string",
    "about": "string",
    "location": "string",
    "birth_date": "string",
    "preference": [
        "string"
    ],
    "gender": "string",
    "phone": "string",
    "email": "string",
    "photo_profile": {
      "url": "string",
      "id": "string"
     },
    "photos": [
        "string", "...", "string"
    ],
    "course": "string",
    "complete_register": "boolean"
}
```
<br/>

status(200): 
```json
{
    "_id": "string",
    "name": "string",
    "lastName": "string",
    "about": "string",
    "location": "string",
    "birth_date": "string",
    "preference": [
        "string", "...", "string"
    ],
    "gender": "string",
    "phone": "string",
    "email": "string",
    "photo_profile": {
      "url": "string",
      "id": "string"
     },
    "photos": [
        "string", "...", "string"
    ],
    "course": "string",
    "complete_register": "boolean"
}
```
<br/>

status(500): Unexpected server error

#

#### Primeira etapa do registro

```http
  PATCH /register_part1
```

| Body   | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `email`      | `string` | **Obrigatório**. E-mail do usuário ou string vazia. |
| `phone`      | `string` | **Obrigatório**. Telefone do usuário ou string vazia. |
| `name`      | `string` | **Obrigatório**. Primeiro nome do usuário. |
| `lastName`      | `string` | **Obrigatório**. Último nome do usuário. |
| `birth_date`      | `number` | **Obrigatório**. Data de nascimento do usuário. |
| `gender`      | `string` | **Obrigatório**. Gênero do usuário. |

#### Retorna 2 possíveis respostas:

status(200): 
```json
{
  "id": "id"
}
```
<br/>

status(500): 
```json
{
  "message": "Cant access the database"
}
```

#

#### Segunda etapa do registro

```http
  POST /register_part2/:id
```

| Params   | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `id`      | `string` | **Obrigatório**. Id do usuário. |

| File   | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `image`      | `file` | **Obrigatório**. Imagem de perfil do usuário. |

#### Retorna 3 possíveis respostas:

status(400): 
```json
{
  "error": "Nenhuma imagem fornecida"
}
```
<br/>

status(201): 
```json
{
    "_id": "string",
    "name": "string",
    "lastName": "string",
    "about": "string",
    "location": "string",
    "birth_date": "string",
    "preference": [
        "string", "...", "string"
    ],
    "gender": "string",
    "phone": "string",
    "email": "string",
    "photo_profile": {
      "url": "string",
      "id": "string"
     },
    "photos": [
        "string", "...", "string"
    ],
    "course": "string",
    "complete_register": "boolean"
}
```
<br/>

status(500): Unexpected server error
