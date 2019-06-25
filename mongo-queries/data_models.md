## Embedded

```js
    // employee document
    {
        _id: ObjectId('123'),
        name: "John Doe",
        contact: {
            email: "john@doe.com",
            phone: '123-456'
        },
        access: {
            level: 5,
            team: 'dev'
        }
    }
```

## Normalized (reference)

```js
    // employee document
    {
        _id: ObjectId('123'),
        name: "John Doe"
    }

    // contact document
    {
        _id: ObjectId('456'),
        email: "john@doe.com",
        phone: '123-456',
        employee_id: ObjectId('123')
    }

    // access document
    {
        _id: ObjectId('789'),
        level: 5,
        team: 'dev',
        employee_id: ObjectId('123')
    }
```

#### One-to-One

with embedded data model

```js

    // normalized

    // user
    {
        _id: ObjectId('1'),
        name: "Björn"
    }

    // ssn
    {
        _id: ObjectId('2'),
        ssn: 42,
        user_id: ObjectId('1')
    }

    =>

    // embedded

    {
        _id: ObjectId('1'),
        name: "Björn",
        ssn: 42
    }

```

#### One-to-Many

with embedded data model

```js

    // normalized

    // customer
    {
        _id: ObjectId('1'),
        name: "Anna"
    }

    // address
    {
        _id: ObjectId('2'),
        street: "sesame",
        city: "NYC",
        customer_id: ObjectId('1')
    }

    // address
    {
        _id: ObjectId('3'),
        street: "EichhornStr 3",
        city: "Berlin",
        customer_id: ObjectId('1')
    }

    =>

    // embedded

    {
        _id: ObjectId('1'),
        name: "Anna",
        addresses: [
            {
                street: "sesame",
                city: "NYC",
            },
            {
                street: "EichhornStr 3",
                city: "Berlin",
            }
        ]
    }

```

with normalized data model

```js
    // embedded

    // book
    {
        _id: ObjectId('123'),
        title: 'The Catcher in the Rye',
        author: 'JD Salinger',
        publisher: {
            name: 'Pinguin'
            founded: 1940,
            location: 'UK'
        }
    }

    // book
    {
        _id: ObjectId('456'),
        title: 'A Long Way Down',
        author: 'Nick Hornby',
        publisher: {
            name: 'Pinguin'
            founded: 1940,
            location: 'UK'
        }
    }

    =>

    // normalized

    // publisher
    {
        _id: ObjectId('789')
        name: 'Pinguin'
        founded: 1940,
        location: 'UK'
    }

    // book
    {
        _id: ObjectId('123'),
        title: 'The Catcher in the Rye',
        author: 'JD Salinger',
        publisher_id: ObjectId('789')
    }

    // book
    {
        _id: ObjectId('456'),
        title: 'A Long Way Down',
        author: 'Nick Hornby',
        publisher_id: ObjectId('789')
    }

```
