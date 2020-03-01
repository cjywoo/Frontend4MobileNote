# 测试

## 远程测试工具
利用vue-remote-devtools

1. 全局安装@vue/devtools
```
npm install -g @vue/devtools
```

2. 使用命令启动
```
vue-devtools
```

3. 将界面上打印出的script标签加载源码中

## 前端自动化测试

### 如何使用jest框架
安装完jest后，使用```npx jest --init``命令，初始化配置，然后使用```jest```命令就会扫描目录下以.test.js的文件进行测试，并生成测试报告。常用命令

```
# 生成配置文件
npx jest --init

# 生成coverage报告
npx jest --coverage

# 一直检测测试用例，修改后，并重新进行测试
npx jest --watchAll
```
### 测试用例格式
必须以.test.js为结尾。

1. 同步函数测试用例
```
import { fetchData } from './fetchData';

test('fetchData 返回结果为 {success:true}', () => {
  fetchData((data) => {
    expect(data).toEqual({
      success: true
    })
  })
})
```

2. 异步回调函数函数测试用例，必须包括done函数
```
import { fetchData } from './fetchData';

test('fetchData 返回结果为 {success:true}', (done) => {
  fetchData((data) => {
    expect(data).toEqual({
      success: true
    })
    done();
  })
})czw
```

3. 异步的promise函数测试用例，需要用return返回
```
test('fetchData 返回结果为 {success:true}', () => {
  return fetchData().then(res => {
    expect(res.data).toEqual({
      success: true
    })
  })
})
```

4. 异步的promise函数测试用例，需要用return返回2
```
test('fetchData 返回结果为 { success: true }', () => {
  return expect(fetchData()).resolves.toMatchObject({
    data: {
      success: true
    }
  })
})
```

5. 只想测试某一个测试用例时，用test.only

### 钩子函数
钩子函数主要由于以下几种
* describe: 分组,并形成自己的作用域
* beforeAll: 所有测试方法之前调用的方法
* beforeEach: 每个测试方法之前调用的方法
* afterAll: 所有测试方法之后调用的方法
* afterEach: 每个测试方法之后调用的方法

```
let counter = null
beforeAll(() => {
  counter = new Counter()
})

beforeEach(() => {
  counter = new Counter()
})

afterAll(() => {
  console.log('测试成功')
})

describe('测试增加相关的代码', () => {
  test('测试 Counter中的 addOne 方法', () => {
    counter.addOne()
    expect(counter.number).toBe(1)
  })
})

describe('测试减少相关的代码', () => {
  test('测试 Counter中的 minusOne 方法', () => {
    counter.minusOne()
    expect(counter.number).toBe(-1)
  })
})
```

### mock函数
1. 捕获函数的调用和返回结果，以及this和调用顺序
2. 可以让我们自由的设置返回结果
3. 改变函数的内部实现，比如axios的发返回结果