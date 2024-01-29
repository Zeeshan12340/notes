# API
In a normal REST api, you might do something like this

`curl cereal.api -d "title='Lucky Charms'"`

and you would receive a JSON response looking like 

`{`  
`"sugar": "50000000g"`  
`"protein": "0g"`  
`...`  
`}`

Given the object Dog, with a parameter of name, how would you query the weight for a Shiba Inu.

{ Dog(name: "Shiba Inu"){weight}}

`{ __type(name: "para"){fields{name}}}` to extract info from graphql