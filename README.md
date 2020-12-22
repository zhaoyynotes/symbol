# ES6 Symbol 使用场景

E66中新增了第7种原始类型Symbol,(原有6种分别是Boolean,Null,Undefined,Number,BigInt,String)
Symbol是js中独一无二的值，可以通过下面的方式创建一个Symbol类型值

```markdown
const s = Symbol();
console.log(s); //'symbol'
```

Symbol方法接收一个参数，表示对生成的symbol的值的一种描述，即使传入相同的参数，生成的symbol值也是不相等的，因为symbol本来就是独一无二的意思
```markdown
const foo = Symbol('foo');
const bar = Symbol('foo');
console.log(foo === bar); //false
```

Symbol.for方法可以检测上下文中是否已经存在该方法且相同参数创建的symbol值，如果存在在返回已经存在的值，如果不存在则新建。
```markdown
const foo = Symbol.for('foo');
const bar = Symbol.for('foo');
console.log(foo === bar); //true
```

Symbol.keyFor方法返回一个使用Symbol.for方法创建的symbol值的key
```markdown
const foo = Symbol.for('foo');
const key = Symbol.keyFor(foo);
console.log(key); //'foo'
```

## 使用场景1.代替常量
```markdown
const TYPE_AUDIO = 'AUDIO'
const TYPE_VIDEO = 'VIDEO'
const TYPE_IMAGE = 'IMAGE'

function handleFileResource(resource) {
  switch(resource.type) {
    case TYPE_AUDIO:
      console.log('playAudio')
      break
    case TYPE_VIDEO:
      console.log('playVideo')
      break
    case TYPE_IMAGE:
      console.log('previewImage')
      break
    default:
      throw new Error('Unknown type of resource')
  }
}
handleFileResource({type:TYPE_AUDIO})
```
有了symbol之后
```markdown
const TYPE_AUDIO = Symbol()
const TYPE_VIDEO = Symbol()
const TYPE_IMAGE = Symbol()
```

## 使用场景2.使用Symbol作为对象属性名
```markdown
const PROP_NAME = Symbol()
const PROP_AGE = Symbol()

let obj = {
  [PROP_NAME]: "一斤代码"
}
obj[PROP_AGE] = 18

obj[PROP_NAME] // '一斤代码'
obj[PROP_AGE] // 18
```

