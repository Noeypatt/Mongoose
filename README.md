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
  const Modelname = mongoose.model('model-name', nameSchema);
```

##Schema
```json
  import mongoose
  const Schema = mongoose.Schema;
  
  export const NameSchema = new Schema(
  {
    name: [Types],
  },
  { Option }
);
```
**Types:** String, Number, Boolean | Bool, Array, Buffer, Date, ObjectId | Oid, Mixed

**Option:**
```json
ex.
  {
    versionKey: false // auto _v
    timestamps: true, // auto createdAt and updatedAt
  }
  
ex2.
  .set //เป็นการ set option เพิ่มใน schema เขียนด้านล่างตัว Schema ที่ export
  NameSchema.set('toJSON', { getters: true }); // การทำงานเหมือน toObject แต่ใช้ได้เฉพาะ เมื่อ Document นั้นมีการใช้ toJSON ภายใน
  NameSchema.set('toObject', { getters: true }); // แปลงข้อมูลที่ได้ให้อยู่ในรูป JavaScript Object
```
