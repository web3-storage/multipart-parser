# multipart-parser

> A simple multipart/form-data parser to use with ReadableStreams

## Install

```sh
# install it as a dependency
$ npm i @web3-storage/multipart-parser
```

# Usage

```js
import { parseMultipart } from '@web3-storage/multipart-parser';

...

async function requestHandler(req) {
    const boundary = '----whatever';
    const parts = await parseMultipart(req.body, boundary);
    const fd = new FormData();
    for (const { name, data, filename, contentType } of parts) {
        if (filename) {
            fd.append(name, new Blob([data], { type: contentType }), filename);
        } else {
            fd.append(name, new TextDecoder().decode(data), filename);
        }
    }
}
```
