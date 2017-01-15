## vue-cli安装

需要已经安装node.js、npm，这里npm用cnpm替换

1.  全局安装vue-cli模块：cnpm install --global vue-cli

2.  安装vue全家桶：vue init webpack my-project
    默认安装的是vue2.0版的，安装1.0：vue init webpack#1.0 my-project
    第四项：选择Vue build：
        运行时+编译环境：Runtime + Compiler: recommended for most users
        仅运行时：Runtime-only: about 6KB lighter min+gzip, but templates (or any Vue-specific HTML) are ONLY allowed in .vue files - render functions are required elsewhere
    第五项：Use ESLint to lint your code? (Y/n)  
        ESLint介绍：用来检查Javascript编程时的语法错误
    第六项：选择Pick an ESLint preset，选择预设的ESLint：
        标准形式：Standard (https://github.com/feross/standard)
        AirBNB形式：AirBNB (https://github.com/airbnb/javascript)
            AirBNB的介绍：A mostly reasonable approach to JavaScript（个人翻译：一个最合理的javascript书写规范）
        自己配置：none (configure it yourself)
    第七项：Setup unit tests with Karma + Mocha? (Y/n)
        Karma介绍：是一个基于Node.js的JavaScript测试执行过程管理工具，浏览器运行项目后监控文件内容的变化自动执行刷新页面。
        Mocha介绍：流行的javascript测试框架，测试代码执行结果是否符合预期。
    第八项：Setup e2e tests with Nightwatch? (Y/n)

3.  进入目录安装依赖：cd my-project | cnpm install

4.  运行：cnpm run dev