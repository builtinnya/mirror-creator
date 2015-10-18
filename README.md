# mirror-creator

Another way to create an object with values equal to its key names.

## Install

Get it via `npm`:

```
npm install --save mirror-creator
```

## Usage

```javascript
// actionTypes.js
import mirrorCreator from 'mirror-creator';

export default mirrorCreator([
  'SOME_ACTION_TYPE',
  'ANOTHER_ACTION_TYPE',
  'ONE_MORE_ACTION_TYPE',
]);

// actionCreator.js
import actionTypes from 'actionTypes';

dispatch({ type: actionTypes.SOME_ACTION_TYPE });
```

**Pros**: DRY & clean.  
**Cons**: If you use Closure Compiler advanced mode for JS minification — keys are not optimized. Use [`keyMirror`](https://github.com/STRML/keyMirror) instead. [Details](https://github.com/facebook/react/issues/1639#issuecomment-45188026).


## Why

Use it if you don't like native or `keyMirror` ways of defining constants in flux / redux apps.

Native way:

```javascript
// actionTypes.js
export const SOME_ACTION_TYPE     = 'SOME_ACTION_TYPE';
export const ANOTHER_ACTION_TYPE  = 'ANOTHER_ACTION_TYPE';
export const ONE_MORE_ACTION_TYPE = 'ONE_MORE_ACTION_TYPE';

// actionCreator.js
import * as actionTypes from 'actionTypes';

dispatch({ type: actionTypes.SOME_ACTION_TYPE });
```

**Pros**: No third-party lib required.  
**Cons**: Duplications. Noisy.


`keyMirror` way:

```javascript
// actionTypes.js
import keyMirror from 'keyMirror';

export default keyMirror({
  SOME_ACTION_TYPE    : null,
  ANOTHER_ACTION_TYPE : null,
  ONE_MORE_ACTION_TYPE: null,
});

// actionCreator.js
import actionTypes from 'actionTypes';

dispatch({ type: actionTypes.SOME_ACTION_TYPE });
```

**Pros**: DRY. If Closure Compiler advanced mode is used — keys are optimized.  
**Cons**: `null` noise.
