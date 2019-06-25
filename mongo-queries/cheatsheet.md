### Basic Query

{ field: value }

{ title: "The Godfather: Part II" } // returns all the documents in the movies collection where the `title` is "The Godfather: Part II"

{ director: "Francis Ford Coppola" } // return all the movies where the `director` is "Francis Ford Coppola"

### Logical Operators

    { $and: [ { field: value }, { field: value }] }

    $and: all the conditions inside the array must match
    { $and: [ { director: "Christopher Nolan" }, { year: "2008" } ] }

    $or: at least one of the conditions inside the array must match
    { $or: [ { director: "Christopher Nolan" }, { year: "2008" } ] }

    $nor: none of the conditions must match
    { $nor: [ { title: /The/ }, { year: "2008" } ] }

### Projections

The PROJECT field allows us to select which fields to be returned in the returned documents.

    { title: 1, _id: 0 } // will return only the titles
    { title: 1 } // will return only the titles and the _id fields

### Sort

We can sort by fields, using the same syntax, -1 for descending order and 1 for ascending

{ year: -1, title: 1 } // sort the movies from the newest and then alphabetically

### Skip and Limit

Skips x documents and limit the search to y documents.
Useful for pagination

### Comparison Operators

> $ne:
{ field: { $ne: value } }

    {year: { $ne: "1974" }} // returns all movies where the year is NOT "1974"

> $gt: 
{ field: { $gt: value }}

    { year: { $gt: "1974" } } // returns all movies where the year is strictly greater than "1974"

> $gte: 
{ field: { $gte: value }}

    { year: { $gte: "1974" } } // returns all movies where the year is greater than "1974" or equal

$lt and $lte for `less than` and `less than or equal`

Combining operators:

    { $and: [ { rate: {$gt: "7"} }, { rate: {\$lt: "8.5"} } ] } // returns all the movies where the rate is strictly greater than "7" and strictly smaller than "8.5"

<!-- Movie.find({ $and: [ { rate: {$gt: "7"} }, { rate: {\$lt: "8.5"} } ] }) -->

### Array operators

> \$in selects the documents where the value at the given field is present in the given array

    { title: { $in: [ "Forrest Gump", "The Godfather", "Drive" ] } } // return all movies where the `title` is either Forrest Gump, The Godfather or Drive

> \$nin selects all the documents where the value at the given field is absent from the given array

    { year: { $nin: [ "1994", "1995" ] } } // return all movies where the year is neither 1994 nor 1995

> \$all selects the documents where the value at a given field is an array that contains all the values in the given array

    { genre: { $all: [ "Crime", "Drama" ] } } // return all movies that have both Crime and Drama in their genre field

### More operators

> \$exists: true or false

Provided a boolean value, will return all the documents that have or don't have a specific field

    {year: { $exists: false }} // returns all movies where the year field doesn't exist

> \$type: type

Provided a mongo data type, will return all the documents where the specific field is of the given type

    {rate: { $type: "double" }} // returns all movies where the value at the `rate` field is of type `double`

“double”
“string”
“object”
“array”
“objectId”
“bool”
“date”
“null”
