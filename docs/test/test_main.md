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
