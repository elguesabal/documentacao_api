
## Documentação da API

#### Envia um código por e-mail para válidação

```http
  POST /send_email
```

| Body   | Tipo       | Descrição                           |
| :---------- | :--------- | :---------------------------------- |
| `email` | `string` | **Obrigatório**. E-mail que receberá o código de verificação. |

#### Retorna 2 possíveis respostas:

status(200): { message: "We sent a confirmation code to your email!" }

status(400): { message: "Enter an existing email!" }

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

status(400): { message: "Invalid or expired code!" }

status(202): { message: "Continue with customer registration" }

status(403): myuser

status(200): myuser

status(500): Unexpected server error

#

#### Primeira etapa do registro

```http
  PATCH /register_part1
```

| Body   | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `email`      | `string` | **Obrigatório**. E-mail do usuário. |
| `phone`      | `?` | **Obrigatório**. Telefone do usuário. |
| `name`      | `string` | **Obrigatório**. Primeiro nome do usuário. |
| `lastName`      | `string` | **Obrigatório**. Último nome do usuário. |
| `birth_date`      | `?` | **Obrigatório**. Data de nascimento do usuário. |
| `gender`      | `string` | **Obrigatório**. Gênero do usuário. |

#### Retorna 2 possíveis respostas:

status(200): { id: id }

status(500): { message: "Cant access the database" }

#

#### Segunda etapa do registro

```http
  POST /register_part2/:id
```

| Params   | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `id`      | `string` | **Obrigatório**. Id do usuário. |
| `phone`      | `?` | **Obrigatório**. Telefone do usuário. |


| File   | Tipo       | Descrição                                   |
| :---------- | :--------- | :------------------------------------------ |
| `buffer`      | `?` | **Obrigatório**. ?. |
| `mimetype`      | `?` | **Obrigatório**. ?. |

#### Retorna 3 possíveis respostas:

status(400): { error: "Nenhuma imagem fornecida" }

status(201): myuser

status(500): { message: "Cant access the database" }
