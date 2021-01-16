# url-loader

```js
import { argc, argv } from 'http://localhost:0'   // Readable Stream
import { log as stdout_log } from 'http://localhost:1'    // Writable Stream
import { log as stderr_log } from 'http://localhost:2'    // Writable Stream
import { format } from 'http://localhost:4/io'  // stdandard library
import { assert } from 'http://localhost:4/assert'
assert(typeof argc === 'number');
assert(typeof argv === 'object' && Array.isArray(argv) === true);

stdout_log(format('argv[0]: {}', argv[0]));
import('http://localhost:4/process').then(exit => {
  stdout_log('byebye~');
  exit(0);
}).catch(() => {
  stderr_log("some goes wrong!");
  throw new Error("some goes wrong!");
});
```

```bash
$ ./main.js foo
argv[0]: foo
byebye~
# when import module wrong
$ ./main.js goo
argv[0]: goo
some goes wrong!
Error: some goes wrong!                         Core Dump
  at <./main.js> 18:9
```

We use `HTTP` protocol on the URL as base of our kernel system, instead of `File Descriptor` on the `Linux` or some other great system.

Each program has it own unique `URLSession`. When your import a System server, `URLSession` will create `URLSessionTask` to load the function that you import.

```text
URLSession -> URLSessionTask -> URLRequest / URLResponse -> Stream -> Socket
```
