
```
domain = infosil.usil.edu.pe

1) Easy to find

after pressing Employees on LINKEDIN (we get an url)

Example: https://portal.usil.edu.pe/alumno/diplomas?ci=2&cp=1&ca=1301426&ga=1

we can fuzz ca=1301426  (IDOR vulnerability found)

2) Medium to find

after pressing Find Wordpress #2 (we get an url)
https://internacional.usil.edu.pe/nacional/wp-content/uploads/2021/06/INTERCAMBIO-VIRTUAL_final.pdf 
we can see uploaded files on

Example : https://internacional.usil.edu.pe/nacional/wp-content/ 
(Directories disclosed vulnerability found)

3) Medium to find

https://internacional.usil.edu.pe/nacional/ (Wordpress found)
so we can press Wordpress users / login and see some dorks, let's test in the above url path 

Example : https://internacional.usil.edu.pe/internacional/wp-json/wp/v2/users/?per_page=100&page=1 (Users Wordpress disclosed vulnerability found)

4) Medium to find

Also we can see Wordpress login going to 

Example : https://internacional.usil.edu.pe/internacional/wp-admin (Login Wordpress vulnerability found)

domain = usil.instructure.com

5) Easy to find

after pressing Search in Web Archive #2 (we get some urls found in the past by Wayback Machine)
so after logging in canvas we can see eportfolios from other users
we can fuzz 1135

Example : https://usil.instructure.com/eportfolios/1135 (IDOR vulnerability found)

6) Hard to find

After testing for some hours I found that after pressing GraphQL we get some dorks
so let's test it with https://usil.instructure.com/graphiql (GraphQL console found)

we can see all schema with this code

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
  type {
    ...TypeRef
  }
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

query IntrospectionQuery {
  __schema {
    queryType {
      name
    }
    mutationType {
      name
    }
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

then we get a response after executing (Ctrl + A to copy all) then paste in 

https://graphql-kit.com/graphql-voyager/ then press CHANGE SCHEMA the paste in INTROSPECTION and finally DISPLAY (GRAPHQL schema vulnerability found)
```

![[Pasted image 20231027213739.png]]

![[Pasted image 20231027213719.png]]

![[Pasted image 20231027214013.png]]

![[Pasted image 20231027214135.png]]
![[Pasted image 20231027215313.png]]

![[Pasted image 20231027214816.png]]
![[Pasted image 20231027215245.png]]
![[Pasted image 20231027215624.png]]
![[Pasted image 20231027215958.png]]![[Pasted image 20231027220155.png]]![[Pasted image 20231027220756.png]]![[Pasted image 20231027220959.png]]
![[Pasted image 20231027221247.png]]
![[Pasted image 20231027221525.png]]
![[Pasted image 20231027221712.png]]

