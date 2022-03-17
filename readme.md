# Type.js
在运行时检查数据的类型

# 使用
##### 安装
``` bash
npm install @ppzp/type
```

##### demo
``` js
const {
  Type,

  NilField,
  UnvalidatedField,
  NilWrongDetail,
  FieldWrongDetail
} = require('@ppzp/type')

const type = new Type([
  {
    name: 'phone',
    validate: 'string'
  }, {
    name: 'gender',
    validate(value) {
      return value == 'male' || value == 'female'
    }
  }, {
    name: 'name',
    notNull: true,
    validate: 'string'
  }
])

const result1 = type.validate({
  phone: 123,
  gender: 'male'
})
console.log(result1.is(FieldWrongDetail)) // true
console.log(result1.name) // "phone"

const result2 = type.validate()
console.log(result2.is(NilWrongDetail)) // true

const result3 = type.validate({})
console.log(result3.is(FieldWrongDetail)) // true
console.log(result3.name) // "name"
console.log(result3.type == NilField) // true

const result4 = type.validate({
  gender: 1
})
console.log(result4.is(FieldWrongDetail)) // true
console.log(result4.name) // "gender"
console.log(result4.type == UnvalidatedField) // true
```

### LICENSE
The author disclaims copyright to this source code.  
[The Unlicense](https://unlicense.org/)