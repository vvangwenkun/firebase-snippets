# Firebase snippets

Dead simple Firebase snippets you will actually use

Here is direct link to marketplace [Firebase snippets](https://marketplace.visualstudio.com/items?itemName=wangwenkun.firebase-js-snippets)

## Supported languages (file extensions)

- JavaScript (.js)

## Basic Methods

| Prefix      | Method                                                              |
| ----------: | -----------------------------------------------------------------   |
| `rfns→`     | `const functions = require('firebase-functions')`                   |
| `rfnsv2→`   | `const functions = require('firebase-functions/v2')`                |
| `radfs→`    | `const firestore = require('firebase-admin/firestore')`             |
| `rgetfns→`  | `const { getFunctions } = require('firebase-admin/functions')`      |
| `rfntest→`  | `const { wrap, mockConfig } = require('firebase-functions-test')()` |
| `tqref→`    | `const queue = getFunctions().taskQueue('taskQueueFunctionName')`   |

## Cloud Functions

### `hcall`

```javascript
exports.funcName = functions.https
  .onCall(async (data, context) => {
    const uid = context?.auth?.uid
    const email = context?.auth?.token?.email
    
    return { code: 0, message: 'success' }
  })
```

### `hcallv2`

```javascript
exports.funcName = functions.https
  .onCall(async (req) => {
    const uid = req?.auth?.uid
    const email = req?.auth?.token?.email
    
    return { code: 0, message: 'success' }
  })
```

### `hreq`

```javascript
exports.funcName = functions.https
  .onRequest(async (req, res) => {
    
    return res.status(200).send({ code: 0, message: 'success' })
  })
```

### `hreqv2`

```javascript
exports.funcName = functions.https
  .onRequest(
    { cors: [], timeoutSeconds: 1200 },
    async (req, res) => {
      
      return res.status(200).send({ code: 0, message: 'success' })
    }
  )
```

### `tqfns`

```javascript
exports.funcName = functions
  .runWith({})
  .tasks.taskQueue({
    retryConfig: {
      maxAttempts: 5,
      minBackoffSeconds: 60,
    },
    rateLimits: {
      maxConcurrentDispatches: 10,
    },
  })
  .onDispatch(async (data) => {

  })
```

### `tqfnsv2`

```javascript
exports.funcName = functions
  .tasks.onTaskDispatched(
    {
      retryConfig: {
        maxAttempts: 5,
        minBackoffSeconds: 60,
      },
      rateLimits: {
        maxConcurrentDispatches: 10,
      },
    },
    async (req) => {
      
    }
  )
```

### `schfns`

```javascript
exports.funcName = functions.pubsub
  .schedule('every 5 minutes')
  .timeZone('America/New_York')
  .onRun(async (context) => {
    
  })
```

### `schfnsv2`

```javascript
exports.funcName = functions.scheduler
  .onSchedule('every day 00:00', async (event) => {
    
  })
```

### `fsdc`

```javascript
exports.funcName = functions.firestore
  .document('users/{userId}')
  .onCreate(async (snapshot, context) => {
    const doc = snapshot.data()
    const { params, eventId, timestamp } = context
    
  })
```

### `fsdcv2`

```javascript
exports.funcName = functions.firestore
  .onDocumentCreated('users/{userId}', (event) => {
    const { data: snapshot, params, id: eventId, time: timestamp } = event
    const data = snapshot.data()
    
  })
```

### `fsdu`

```javascript
exports.funcName = functions.firestore
  .document('users/{userId}')
  .onUpdate(async (change, context) => {
    const before = change.before.data()
    const after = change.after.data()
    const { params, eventId, timestamp } = context
    
  })
```

### `fsduv2`

```javascript
exports.funcName = functions.firestore
  .onDocumentUpdated('users/{userId}', async (event) => {
    const { data, params, id: eventId, time: timestamp } = event
    const before = data.before.data()
    const after = data.after.data()
    
  })
```

### `fsdd`

```javascript
exports.funcName = functions.firestore
  .document('users/{userId}')
  .onDelete(async (snapshot, context) => {
    const doc = snapshot.data()
    const { params, eventId, timestamp } = context
    
  })
```

### `fsddv2`

```javascript
exports.funcName = functions.firestore
  .onDocumentDeleted('users/{userId}', async (event) => {
    const { data: snapshot, params, id: eventId, time: timestamp } = event
    const data = snapshot.data()
    
  })
```

### `fsdw`

```javascript
exports.funcName = functions.firestore
  .document('users/{userId}')
  .onWrite(async (change, context) => {
    const before = change.before.exists ? change.before.data() : null
    const after = change.after.exists ? change.after.data() : null
    const { params, eventId, eventType, timestamp } = context
    
  })
```

### `fsdwv2`

```javascript
exports.funcName = functions.firestore
  .onDocumentWritten('users/{userId}', async (event) => {
    const { data, params, id: eventId, time: timestamp } = event
    const before = data.before.exists ? data.before.data() : null
    const after = data.after.exists ? data.after.data() : null
    
  })
```

### `rtdbc`

```javascript
exports.funcName = functions.database
  .ref('/foo/{bar}')
  .onCreate(async (snapshot, context) => {
    const value = snapshot.val()
    const { params, eventId, timestamp } = context
    
  })
```

### `rtdbcv2`

```javascript
exports.funcName = functions.database
  .onValueCreated('/foo/{bar}', async (event) => {
    const value = event.data.val()
    const { params, id: eventId, time: timestamp } = event
    
  })
```

### `rtdbu`

```javascript
exports.funcName = functions.database
  .ref('/foo/{bar}')
  .onUpdate(async (change, context) => {
    const before = change.before.val()
    const after = change.after.val()
    const { params, eventId, timestamp } = context
    
  })
```

### `rtdbuv2`

```javascript
exports.funcName = functions.database
  .onValueUpdated('/foo/{bar}', async (event) => {
    const { data, params, id: eventId, time: timestamp } = event
    const before = data.before.val()
    const after = data.after.val()
    
  })
```

### `rtdbd`

```javascript
exports.funcName = functions.database
  .ref('/foo/{bar}')
  .onDelete(async (snapshot, context) => {
    const value = snapshot.val()
    const { params, eventId, timestamp } = context
    
  })
```

### `rtdbdv2`

```javascript
exports.funcName = functions.database
  .onValueDeleted('/foo/{bar}', async (event) => {
    const value = event.data.val()
    const { params, id: eventId, time: timestamp } = event
    
  })
```

### `rtdbw`

```javascript
exports.funcName = functions.database
  .ref('/foo/{bar}')
  .onWrite(async (change, context) => {
    const before = change.before.exists() ? change.before.val() : null
    const after = change.after.exists() ? change.after.val() : null
    const { params, eventId, eventType, timestamp } = context
    
  })
```

### `rtdbwv2`

```javascript
exports.funcName = functions.database
  .onValueWritten('/foo/{bar}', async (event) => {
    const { data, params, id: eventId, time: timestamp } = event
    const before = data.before.exists() ? data.before.val() : null
    const after = data.after.exists() ? data.after.val() : null
    
  })
```

### `rcfns`

```javascript
exports.funcName = functions.remoteConfig
  .onUpdate(async (versionMetadata) => {
    const currentVersion = versionMetadata.versionNumber
    
  })
```

### `rcfnsv2`

```javascript
exports.funcName = functions.remoteConfig
  .onConfigUpdated(async (event) => {
    const currentVersion = event.data.versionNumber
    
  })
```

### `pbfns`

```javascript
exports.funcName = functions.pubsub
  .topic('topicName')
  .onPublish(async (message, context) => {
    const messageBoy = message.data ? Buffer.from(message.data, 'base64').toString() : null
    const { eventId, timestamp } = context
    
  })
```

### `pbfnsv2`

```javascript
exports.funcName = functions.pubsub
  .onMessagePublished('topicName', async (event) => {
    const { data: { message }, id: eventId, time: timestamp } = event
    const messageBoy = message.data ? Buffer.from(message.data, 'base64').toString() : null
    
  })
```