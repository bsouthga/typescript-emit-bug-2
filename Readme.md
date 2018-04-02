# Typescript emit issue

Tested on versions

- 2.7.2
- 2.8.1
- next

## Repro

- install deps (`npm install`)
- run test (`npm test`)
- take a look at `./dist/b.js`

## Description

Given `a.js`  and `b.js` as follows:

```javascript
// a.js
const Obj = {};
export default Obj;
```

```javascript
// b.js
import Obj from './a';

Obj.fn = function() {};
```

The following emit is produced for `b.js` -- missing the import of `Obj` and
resulting in a runtime error:

```javascript
"use strict";
Object.defineProperty(exports, "__esModule", { value: true });
Obj.fn = function () { };
//# sourceMappingURL=b.js.map
```