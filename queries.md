
**names only**
db.restaurants.find({}, {id: false, name: true})

**number of bakeries starting with M**
db.restaurants.find({$and: [{cuisine: "Bakery"}, {name: /^M/}]}).count()

**names with ICE, but show only zip codes and id**
db.restaurants.find({cuisine: /Ice/}, {"address.zipcode": true})

**Chinese restaurant addresses sorted by zip code**
db.restaurants.find({cuisine: "Chinese"}, {"address.building": true, "address.street": true}).sort({"address.zipcode": 1})

**American cuisine in Manhattan**
db.restaurants.find({"cuisine": "American ", "borough": "Manhattan"})

**Received 4 grades**
db.restaurants.find({"grades": {$size:4}})

**Name of Broadway places with two grades**
db.restaurants.find({"address.street": /Broadway/}, {grades: {$slice: 2}, name: true})

**5 high-scoring Bronx pizza restaurants**
db.restaurants.find({"borough": /Bronx/, "cuisine": "Pizza"}).sort({"grades.score": -1}).limit(5)

**last ten of 60 alphabetical Brooklyn restaurants**
db.restaurants.find({borough: "Brooklyn", name: /^[A-Za-z][A-Za-z0-9]/}, {name: 1}).sort({"name": -1}).skip(20).limit(10)

**italian or pizza places, reverse alpahbetical**
db.restaurants.find({$or:[{"cuisine": "Pizza", "cuisine": "Italian"}]}).sort({"name": -1})