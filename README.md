# Mongoose

Getting Started

- ติดตั้ง mongoose
```bash
  $ npm install mongoose --save
```

- เชื่อมต่อ database (mongoDB)
```mongoose
  import mongoose
  mongoose.connect('mongodb://localhost:27017/database-name');
```

- สร้าง Schema
```mongoose
  const nameSchema = new mongoose.Schema({
    [key]: [Type]
  });
```

- สร้าง Model
```mongoose
  const Modelname = mongoose.model('model-name', nameSchema);
```

---

##Schema
```mongoose
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
```mongoose
ex.
  {
    versionKey: false,
    timestamps: true,
  }
  versionKey: auto _v
  timestamps: auto createdAt and updatedAt
  
ex2.
  .set //เป็นการ set option เพิ่มใน schema เขียนด้านล่างตัว Schema ที่ export
  NameSchema.set('toJSON', { getters: true }); // การทำงานเหมือน toObject แต่ใช้ได้เฉพาะ เมื่อ Document นั้นมีการใช้ toJSON ภายใน
  NameSchema.set('toObject', { getters: true }); // แปลงข้อมูลที่ได้ให้อยู่ในรูป JavaScript Object
```

---

## Document
1. populate(path,[model],[match],[select],[options],[callback]) 
  - path: ชื่อ fieldObject ที่ต้องการ
  - model: ชื่อ Model ที่จะไปเอาค่า fieldObject มา (import และประกาศใช้ Model ด้วย)  และไม่จำเป็นต้องใส่ค่านี้นี้ ถ้า fieldObject ไม่ได้ต้อง import มาจาก Model อื่น
  - match: { เงื่อนไขตัวดำเนินการเปรียบเทียบ } => เหมือน $match
  - select: 'keyที่ต้องการให้แสดง, -keyที่ไม่ต้องการให้แสดง'
  - options: { limit: 2 }

```mongoose

  Modelname.find().populate({
    path: '',
    model: nameOtherModel
    match: {}, 
    select: ''
    options: {}
  }
  
```

2. save()

```mongoose
  const newModel = ModuleName.create(data)
  
  newModel.save()
```

---

## Model
- การใช้งาน `Model.__`

1. aggregate(): ใช้เหมือน .aggregate([stage]) ของ mongo
2. count(): ใช้นับจำนวน โดยสามารถใส่ filter ได้ `Model.count({type:"A"})` => จำนวนข้อมูลทั้งหมดที่มี type = A
**create**
3. create(): สร้าง docs ต้อง save() ด้วย
**delete**
4. deleteMany({เงื่อนไข}): ลบมากกว่า 1 docs (Hard Delete) 
5. deleteOne({เงื่อนไข}):  ลบ 1 doc (Hard Delete) 
6. findByIdAndDelete(`{_id:id},{เงื่อนไข}`): ค้นหา id ที่ตรงกัน และทำการลบ (Soft Delete) 
7. findByIdAndRemove(`{_id:id},{เงื่อนไข}`): ค้นหา id ที่ตรงกัน และทำการลบ (Hard Delete) 
8. findOneAndDelete({เงื่อนไข}): deleteOne()
9. findOneAndRemove({เงื่อนไข}): deleteOne()
10. remove({เงื่อนไข}): ลบ docs ทั้งหมดที่ตรงเงื่อนไข ถ้าจะให้ลบแค่อันแรกที่เจออันเดียวให้เซ็ท `single:true`(Hard Delete)
**find**
11. find(): ค้นหา และคืนค่าเป็นข้อมูลทั้งหมดที่หาเจอ, สามารถใส่ {เงื่อนไข} ได้
12. findById(): ค้นหาด้วย id และคืนค่าเป็นข้อมูลตัวแรกที่หาเจอ, สามารถใส่ {เงื่อนไข} ได้
13. findOne(): ค้นหา และคืนค่าเป็นข้อมูลตัวแรกที่หาเจอ
**update**
14. update()
15. updateMany()
16. findByIdAndUpdate(`{_id:id},newData,{new:true}`): ค้นหา id ที่ตรงกัน และทำการอัปเดตค่า
17. findOneAndUpdate(`{เงื่อนไข},newData,{new:true}`): อัปเดตค่าที่ตรงเงื่อนไขค่าแรกที่เจอ
18. findOneAndReplace(): 
19. replaceOne(): 
**other**
21. validate({ [field]: null }, ['field']): ตรวจสอบข้อมูล //field นี้ ห้ามเป็น null
22. where(): ใช้ find() แทนได้เหมือนกัน
23. populate(): ใช้เมื่อต้องการ pop ค่าออกมา

