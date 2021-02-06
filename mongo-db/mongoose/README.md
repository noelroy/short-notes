# Mongoose - NodeJS MondoDB Driver

## DB Connection

```
const mongoose = require('mongoose')
mongoose
    .connect(process.env.MONGO_URL, {
        useNewUrlParser: true,
        useUnifiedTopology: true
    })
    .then(() => console.log('Connected to db'))
    .catch(() => console.log(err))
```

