在vue的底层是通过Object.defineProperty()来定义对象属性内部的getter,setter方法
对于一个属性,如果该属性的writable属性为false的话,该属性在被调用的时候其实是调用该属性的get方法
而该属性被赋值的时候,就是调用了该属性的set方法
由于get,方法和set方法在属性被调用和赋值之前可以进行一系列操作,这样就可以实现对数据的劫持操作
让我们来用一个案例来了解一下
```
    <script>
        const obj = {}
        var _message = "大家好我是电棍"
        Object.defineProperty(obj, 'message', {
            enumerable: true,
            configurable: true,
            get() {
                console.log('调用了getter方法')
                return _message;
            },
            set(val) {
                console.log('调用了setter方法')
                _message = val
            }
        })
        console.log(obj.message)
        console.log(obj.message = "这把得拿下啊")
    </script>
```
我可看到,对属性调用和赋值时,其实是执行的该属性的set和get方法