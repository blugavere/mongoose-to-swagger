[![NPM version][npm-image]][npm-url]

# mongoose-to-swagger 

Conversion library for transforming [Mongoose](http://mongoosejs.com/) schema objects into [Swagger](http://swagger.io) schema definitions.

## Installation

```sh
$ npm install --save mongoose-to-swagger-2
```

## Overview

Converts a mongoose model into a swagger schema.
在mongoose-to-swagger库的基础上修正数组的enum转换，enum移到items的定义。

## Usage

```js
const mongoose = require('mongoose');
const m2s = require('mongoose-to-swagger');
const Cat = mongoose.model('Cat', { name: String });
const swaggerSchema = m2s(Cat);
console.log(swaggerSchema);
```

### Meta properties

By default, `description`, `enum`, and `required` fields are extracted from the mongoose schema definitions and placed into the correspoding swagger properties definitions. Additional meta props can be whitelisted using the props array on the options argument.

```ts

const Cat = mongoose.model('Cat', { 
    name: {
        type: String,
        /**
         * Custom Properties
         * `description` is enabled by default
         */
        description: 'Name of the cat', // description is enabled by default
        bar: 'baz' // custom prop
    },
    color: String
});

const options = { 
    /**
     * Whitelist of custom meta fields.
     */
    props: ['bar'],
    /**
     * Fields to omit from model root. "__v" and "id" are omitted by default with omitMongooseInternals (default: true)
     */
    omitFields: ['_id', 'color'], 
    /**
     * Omit mongoose internals, omits mongoose internals from result ("__v", "id" - mongoose version field and virtual id field) (default: true)
     */
    omitMongooseInternals: false
};

const swaggerSchema = m2s(Cat, options);

```



## Contributing
We look forward to seeing your contributions!


## License

MIT © [Ben Lugavere](https://benlugavere.com/)

[npm-image]: https://badge.fury.io/js/mongoose-to-swagger.svg
[npm-url]: https://npmjs.org/package/mongoose-to-swagger
