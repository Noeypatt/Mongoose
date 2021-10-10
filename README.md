# Mongoose

Getting Started

- ติดตั้ง mongoose
```bash
  $ npm install mongoose --save
```

- เชื่อมต่อ database (mongoDB)
```json
  import mongoose
  mongoose.connect('mongodb://localhost:27017/database-name');
```

- สร้าง Schema
```json
  const nameSchema = new mongoose.Schema({
    [key]: [Type]
  });
```

- สร้าง Model
```json
  const Modelname = mongoose.model('model-name', kittySchema);
```
