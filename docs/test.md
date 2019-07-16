# 前端测试

---

> 有效的单元测试是减少你软件错误的一部分。

在实际项目开发中，我们经常发现自己写的代码拿到测试那边进行集成测试或者进行系统测试的时候会被提出很多的简单的 bug，而这些 bug 完全通过我们自己编写单元测试可以避免。下边就记录一下怎样进行单元测试。

## 前端测试框架

### Jasmine

我认为最好用的测试框架(主要是 VUE 官网上用的这个)，语法极其简单，下边开箱使用！

1.  安装 Jasmine

    你可以使用全局安装或者是使用在当前项目中安装

    ```javascript
    npm i jasmine -g jasmine    //全局安装
    npm i jasmin -D             //安装在当前的项目中
    ```

2.  初始化项目

    下边开始初始化一个测试项目

    ```javascript
    jasmine init                                //如果你是全局安装了jasmine
    node node_modules/jasmine/bin/jasmine init  //如果在当前项目中安装了jasmine
    ```

3.  自己生成一个实例

    ```javascript
    jasmine example //如果你是全局安装了jasmine
    node node_modules/jasmine/bin/jasmine example//如果在当前项目中安装了jasmine
    ```

    下边我们开始几个有重要的方法介绍：

    1. describe( String , Function) 函数:

        用于对相关规范进行分组，通常每个测试文件在顶层都有一个。

        string 参数用于命名规范集合，并将与 specs 连接以生成规范的全名。

4.  简单测试例子
    ```javascript
    describe("A suite", function() {
        //没有通过验证，会提示这个语句
        it("contains spec with an expectation", function() {
            //验证，期望是true
            expect(true).toBe(true);
        });
    });
    ```

## VUE 项目的测试
