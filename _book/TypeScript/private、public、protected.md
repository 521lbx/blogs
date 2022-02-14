### private、public、protected

1. 默认为public

2. 当成员被标记为private时，它就不能在声明它的类的外部访问，比如：

```
class Animal {
  private name: string;
  constructor(theName: string) {
    this.name = theName;
  }
}

let a = new Animal('Cat').name; //错误，‘name’是私有的
```

3. protected和private类似，但是，protected成员在派生类中可以访问

```
class Animal {
  protected name: string;
  constructor(theName: string) {
    this.name = theName;
  }
}

class Rhino extends Animal {
  constructor() {
    super('Rhino');
  }         
  getName() {
    console.log(this.name) //此处的name就是Animal类中的name
  }
} 
```

4. 当构造函数被标记为protected。这意味着这个类不能被实例化，但是能被继承，也就是可以在派生类中被super执行

```
class Animal {
  protected name: string;
  protected constructor(theName: string) {
    this.name = theName;
  }
}

//Rhino能够继承Animal
class Rhino extends Person {
  private food: string;
  constructor(name: string, food: string) {
    super(name);
    this.food = food;
  }
  getFood() {
    return `${this.name} love this ${this.food}`
  }
}

let rhino = new Rhino('zhao', 'banana');
```