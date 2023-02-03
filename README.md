# tezos-schema
A public place to field feedback and releases of metadata schema for Tezos storage artifacts.

We're using **GitHub discussions** to field questions/improvements/suggestions for this repo.  Feel free to [open a discussion](https://github.com/oxheadalpha/tezos-schema/discussions) and we'll turn it into an issue, and eventually- a release.

- [tezos-schema](#tezos-schema)
  - [Validate your own metadata](#validate-your-own-metadata)
    - [bash](#bash)
    - [python](#python)
    - [go](#go)
    - [npm/\*script](#npmscript)

## Validate your own metadata

### bash

https://github.com/python-jsonschema/check-jsonschema

```bash
pip install check-jsonschema
check-jsonschema --schemafile https://raw.githubusercontent.com/oxheadalpha/tezos-snapshot-metadata-schema/main/tezos-snapshot-metadata.schema.json input.json
ok -- validation done
```

### python

https://pypi.org/project/jsonschema/

```python
from jsonschema import validate
import json

f = open('schema.json')
schema = json.load(f)

f = open('input.json')
input = json.load(f)

validate(input,schema=schema)
# returns nothing if valid
```

### go

https://github.com/xeipuuv/gojsonschema

```go
package main

import (
    "fmt"
    "github.com/xeipuuv/gojsonschema"
)

func main() {

    schemaLoader := gojsonschema.NewReferenceLoader("file:///home/me/schema.json")
    documentLoader := gojsonschema.NewReferenceLoader("file:///home/me/document.json")

    result, err := gojsonschema.Validate(schemaLoader, documentLoader)
    if err != nil {
        panic(err.Error())
    }

    if result.Valid() {
        fmt.Printf("The document is valid\n")
    } else {
        fmt.Printf("The document is not valid. see errors :\n")
        for _, desc := range result.Errors() {
            fmt.Printf("- %s\n", desc)
        }
    }
}
// Returns "The document is valid" if sucessful
```

### npm/*script

https://www.npmjs.com/package/jsonschema

```bash
npm install jsonschema
```

```javascript
var validate = require('jsonschema').validate;
var schema = JSON.parse(fs.readFileSync('schema.json'))
var input = JSON.parse(fs.readFileSync('input.json'))
validate(input,schema)
```
