# Firebase snippets

Dead simple Firebase snippets you will actually use

Here is direct link to marketplace [Firebase snippets](https://marketplace.visualstudio.com/items?itemName=wangwenkun.firebase-js-snippets)

## Supported languages (file extensions)

- JavaScript (.js)

## Firebase Admin
| Prefix  | Method                                                         |
| ------: | -------------------------------------------------------------- |
| `refs→` | `const firestore = require('firebase-admin/firestore')`        |
| `regfn→` | `const { getFunctions } = require('firebase-admin/functions')` |
| `restg`  | `const { getStorage } = require('firebase-admin/storage')`     |

## Firebase Functions

| Prefix      | Method                                                              |
| ----------: | ------------------------------------------------------------------- |
| `refn→`     | `const functions = require('firebase-functions')`                   |
| `refnv2→`   | `const functions = require('firebase-functions/v2')`                |
| `refntest→` | `const { wrap, mockConfig } = require('firebase-functions-test')()` |
| `tqref→`    | `const queue = getFunctions().taskQueue('taskQueueFunctionName')`   |

## Google Cloud

| Prefix   | Method                                               |
| -------: | ---------------------------------------------------- |
| `reps→`  | `const { PubSub } = require('@google-cloud/pubsub')` |

### `pubmsg`

```javascript
new PubSub({ projectId: 'projectId' })
  .topic('topicName')
  .publishMessage({

  })
```

### `submsg`

```javascript
new PubSub({ projectId: 'projectId' })
  .topic('topicName')
  .subscription('subscriptionName')
  .on('message', async (message) => {
    const messageBoy = message.data ? Buffer.from(message.data, 'base64').toString() : null
    
  })
```

## Cloud Functions

### `hoc`

```javascript
exports.funcName = functions.https
  .onCall(async (data, context) => {
    const uid = context?.auth?.uid
    const email = context?.auth?.token?.email
    
    return { code: 0, message: 'success' }
  })
```

### `hocv2`

```javascript
exports.funcName = functions.https
  .onCall(async (req) => {
    const uid = req?.auth?.uid
    const email = req?.auth?.token?.email
    
    return { code: 0, message: 'success' }
  })
```

### `hoq`

```javascript
exports.funcName = functions.https
  .onRequest(async (req, res) => {
    
    return res.status(200).send({ code: 0, message: 'success' })
  })
```

### `hoqv2`

```javascript
exports.funcName = functions.https
  .onRequest(
    { cors: [], timeoutSeconds: 1200 },
    async (req, res) => {
      
      return res.status(200).send({ code: 0, message: 'success' })
    }
  )
```

### `tqdp`

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

### `tqdpv2`

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

### `schrun`

```javascript
exports.funcName = functions.pubsub
  .schedule('every 5 minutes')
  .timeZone('America/New_York')
  .onRun(async (context) => {
    
  })
```

### `schrunv2`

```javascript
exports.funcName = functions.scheduler
  .onSchedule('every day 00:00', async (event) => {
    
  })
```

### `fsodc`

```javascript
exports.funcName = functions.firestore
  .document('users/{userId}')
  .onCreate(async (snapshot, context) => {
    const doc = snapshot.data()
    const { params, eventId, timestamp } = context
    
  })
```

### `fsodcv2`

```javascript
exports.funcName = functions.firestore
  .onDocumentCreated('users/{userId}', (event) => {
    const { data: snapshot, params, id: eventId, time: timestamp } = event
    const data = snapshot.data()
    
  })
```

### `fsodu`

```javascript
exports.funcName = functions.firestore
  .document('users/{userId}')
  .onUpdate(async (change, context) => {
    const before = change.before.data()
    const after = change.after.data()
    const { params, eventId, timestamp } = context
    
  })
```

### `fsoduv2`

```javascript
exports.funcName = functions.firestore
  .onDocumentUpdated('users/{userId}', async (event) => {
    const { data, params, id: eventId, time: timestamp } = event
    const before = data.before.data()
    const after = data.after.data()
    
  })
```

### `fsodd`

```javascript
exports.funcName = functions.firestore
  .document('users/{userId}')
  .onDelete(async (snapshot, context) => {
    const doc = snapshot.data()
    const { params, eventId, timestamp } = context
    
  })
```

### `fsoddv2`

```javascript
exports.funcName = functions.firestore
  .onDocumentDeleted('users/{userId}', async (event) => {
    const { data: snapshot, params, id: eventId, time: timestamp } = event
    const data = snapshot.data()
    
  })
```

### `fsodw`

```javascript
exports.funcName = functions.firestore
  .document('users/{userId}')
  .onWrite(async (change, context) => {
    const before = change.before.exists ? change.before.data() : null
    const after = change.after.exists ? change.after.data() : null
    const { params, eventId, eventType, timestamp } = context
    
  })
```

### `fsodwv2`

```javascript
exports.funcName = functions.firestore
  .onDocumentWritten('users/{userId}', async (event) => {
    const { data, params, id: eventId, time: timestamp } = event
    const before = data.before.exists ? data.before.data() : null
    const after = data.after.exists ? data.after.data() : null
    
  })
```

### `rtdbodc`

```javascript
exports.funcName = functions.database
  .ref('/foo/{bar}')
  .onCreate(async (snapshot, context) => {
    const value = snapshot.val()
    const { params, eventId, timestamp } = context
    
  })
```

### `rtdbodcv2`

```javascript
exports.funcName = functions.database
  .onValueCreated('/foo/{bar}', async (event) => {
    const value = event.data.val()
    const { params, id: eventId, time: timestamp } = event
    
  })
```

### `rtdbodu`

```javascript
exports.funcName = functions.database
  .ref('/foo/{bar}')
  .onUpdate(async (change, context) => {
    const before = change.before.val()
    const after = change.after.val()
    const { params, eventId, timestamp } = context
    
  })
```

### `rtdboduv2`

```javascript
exports.funcName = functions.database
  .onValueUpdated('/foo/{bar}', async (event) => {
    const { data, params, id: eventId, time: timestamp } = event
    const before = data.before.val()
    const after = data.after.val()
    
  })
```

### `rtdbodd`

```javascript
exports.funcName = functions.database
  .ref('/foo/{bar}')
  .onDelete(async (snapshot, context) => {
    const value = snapshot.val()
    const { params, eventId, timestamp } = context
    
  })
```

### `rtdboddv2`

```javascript
exports.funcName = functions.database
  .onValueDeleted('/foo/{bar}', async (event) => {
    const value = event.data.val()
    const { params, id: eventId, time: timestamp } = event
    
  })
```

### `rtdbodw`

```javascript
exports.funcName = functions.database
  .ref('/foo/{bar}')
  .onWrite(async (change, context) => {
    const before = change.before.exists() ? change.before.val() : null
    const after = change.after.exists() ? change.after.val() : null
    const { params, eventId, eventType, timestamp } = context
    
  })
```

### `rtdbodwv2`

```javascript
exports.funcName = functions.database
  .onValueWritten('/foo/{bar}', async (event) => {
    const { data, params, id: eventId, time: timestamp } = event
    const before = data.before.exists() ? data.before.val() : null
    const after = data.after.exists() ? data.after.val() : null
    
  })
```

### `rcou`

```javascript
exports.funcName = functions.remoteConfig
  .onUpdate(async (versionMetadata, context) => {
    const currentVersion = versionMetadata.versionNumber
    
  })
```

### `rcouv2`

```javascript
exports.funcName = functions.remoteConfig
  .onConfigUpdated(async (event) => {
    const currentVersion = event.data.versionNumber
    
  })
```

### `msgop`

```javascript
exports.funcName = functions.pubsub
  .topic('topicName')
  .onPublish(async (message, context) => {
    const messageBoy = message.data ? Buffer.from(message.data, 'base64').toString() : null
    const { eventId, timestamp } = context
    
  })
```

### `msgopv2`

```javascript
exports.funcName = functions.pubsub
  .onMessagePublished('topicName', async (event) => {
    const { data: { message }, id: eventId, time: timestamp } = event
    const messageBoy = message.data ? Buffer.from(message.data, 'base64').toString() : null
    
  })
```

### `soupl`

```javascript
getStorage().bucket().upload('filePath', { destination: 'destFileName' })
  .then((res) => {
    
  })
  .catch((err) => {
    
  })
```

### `sodown`

```javascript
getStorage().bucket().file().download({ destination: 'destFileName' })
  .then((res) => {
    
  })
  .catch((err) => {
    
  })
```

### `sooa`

```javascript
exports.funcName = functions.storage
  .bucket('bucketName')
  .object()
  .onArchive(async(object, context) => {
    const { bucket: fileBucket, name: filePath, contentType } = object
    
  })
```

### `sooav2`

```javascript
exports.funcName = functions.storage
  .onObjectArchived({ bucket: 'bucketName', }, async(event) => {
    const { bucket: fileBucket, name: filePath, contentType } = event.data
    
  })
```

### `sood`

```javascript
exports.funcName = functions.storage
  .bucket('bucketName')
  .object()
  .onDelete(async(object, context) => {
    const { bucket: fileBucket, name: filePath, contentType } = object
    
  })
```

### `soodv2`

```javascript
exports.funcName = functions.storage
  .onObjectDeleted({ bucket: 'bucketName', }, async(event) => {
    const { bucket: fileBucket, name: filePath, contentType } = event.data
    
  })
```

### `soof`

```javascript
exports.funcName = functions.storage
  .bucket('bucketName')
  .object()
  .onFinalize(async(object, context) => {
    const { bucket: fileBucket, name: filePath, contentType } = object
    
  })
```

### `soof2`

```javascript
exports.funcName = functions.storage
  .onObjectFinalized({ bucket: 'bucketName', }, async(event) => {
    const { bucket: fileBucket, name: filePath, contentType } = event.data
    
  })
```

### `somu`

```javascript
exports.funcName = functions.storage
  .bucket('bucketName')
  .object()
  .onMetadataUpdate(async(object, context) => {
    const { bucket: fileBucket, name: filePath, contentType } = object
    
  })
```

### `somuv2`

```javascript
exports.funcName = functions.storage
  .onObjectMetadataUpdated({ bucket: 'bucketName', }, async(event) => {
    const { bucket: fileBucket, name: filePath, contentType } = event.data
    
  })
```
