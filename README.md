## 部署laravel + vue
## 一、下载工具：composer，npm
## 查看下载工具镜像地址：
## composer:	composer config -g -l repo.packagist
## npm: 	npm get registry 
## 配置阿里镜像：
## composer: 
## composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
（此处安装7.x版本，需要php>=7.2.5）
## npm:
## npm config set registry http://registry.npm.taobao.org/
## Ps：
可在composer.json中设置数据源，先访问第一个，找不到再访问第二个，依次进行，packagist最后一个执行，优先执行其他。
"repositories": {
    "packagist": {
        "type": "composer",
        "url": "https://mirrors.aliyun.com/composer/"
    },
    "1": {
        "type": "composer",
        "url": "https://asset-packagist.org"
    }
}
## 二、安装项目
安装laravel最新版本
composer create-project --prefer-dist laravel/laravel 项目名称
安装vue脚手架
composer require laravel/ui --dev(下载laravel/ui包)
php artisan ui vue
安装node依赖包（可在package.json中进行配置）
npm install
wepack配置文件：此处使用laravel-mix，具体使用方法查看文档：												https://learnku.com/docs/laravel/7.x/mix/7473
三、编写入口文件
后端指定views中入口文件，文件中引入打包后css和js文件（默认路由	/css/app.css，/js/app.js，webpack.mix.js中默认打包路径为跟目录下public/js,public/css）；
四、开发文档
编译项目
npm run dev（开发模式）
npm run pro（生产模式）
启动项目
php artisan serve(本地搭建apache等服务器可按服务器配置启动)
开发规范：(度娘的一套开发规范，比较合理)
一 命名规范
1 项目命名
全部采用小写方式， 以下划线分隔。 例：
my_project_name
2 目录命名
2.1 文件夹
参照项目命名规则； 有复数结构时，要采用复数命名法。
scripts 、 styles 、 images 、 data_models
2.2 文件
2.2.1 JS文件命名
使用分隔符线 如果为单个单词，使用小写md5.js
resize-event.js
2.2.2 CSS, SCSS文件命名
css使用下划线
jdc.scss、jdc_list.scss、jdc_detail.scss
scss使用下划线开头 @import 引入的文件不需要开头的'_'和结尾的'.scss'；
/* not good */@import "_dialog.scss";/* good */@import "dialog";
2.2.3 HTML文件命名
使用下划线
jdc.htmljdc_list.htmljdc_detail.html
scss使用下划线开头 @import 引入的文件不需要开头的'_'和结尾的'.scss'；
/* not good */@import "_dialog.scss";/* good */@import "dialog";
2.3 组件
组件名为多个单词 （这样做可以避免跟现有的以及未来的 HTML 元素相冲突，因为所有的 HTML 元素名称都是单个单词的。）
基础组件名比如 Base、App 或 V。
components/
|- BaseButton.vue
|- BaseTable.vue
|- BaseIcon.vue
components/
|- AppButton.vue
|- AppTable.vue
|- AppIcon.vue
components/
|- VButton.vue
|- VTable.vue
|- VIcon.vue
单例组件名只应该拥有单个活跃实例的组件应该以 The 前缀命名，以示其唯一性。
components/
|- TheHeading.vue
|- TheSidebar.vue
紧密耦合的组件名和父组件紧密耦合的子组件应该以父组件名作为前缀命名。
components/
|- TodoList.vue
|- TodoListItem.vue
|- TodoListItemButton.vue
components/
|- SearchSidebar.vue
|- SearchSidebarNavigation.vue
3 普通变量
命名方法 ：驼峰命名法 命名是复数的时候需要加s
4 常量
命名方法 : 全部大写 命名规范 : 使用大写字母匈牙利式命名法。
const MAX_COUNT = 10const URL = 'https://www.shun178.com'
注意：变量命名要尽量做到见名知意（不懂单词去有道翻译或者去CODELF变量名起名网站查询）
二 注释规范
务必添加注释列表
公共组件使用说明
各组件中重要函数或者类说明
复杂的业务逻辑处理说明
特殊情况的代码处理说明,对于代码中特殊用途的变量、存在临界值、函数中使用的 hack、使用
了某种算法或思路等需要进行注释描述
多重 if 判断语句
注释块必须以/（至少两个星号）开头/
单行注释使用//
三 编码规范
1 指令规范
v-for 循环必须加上 key 属性，在整个 for 循环中 key 需要唯一 避免 v-if 和 v-for 同时用在一个元素上（性能问题）
<ul><li v-for="todo in todos" :key="todo.id"> {{ todo.text }} </li></ul>
四 文档目录结构规范
1 公共组件
存放在 resources\js\components文件夹下面,在该文件夹下的readme.md文档文件中标注自己开发的组件及使用说明
2 页面文件
存放在resources\js\routes下，分模块存放
3 配置及路由文件
存放在 resources\js\config下
4 静态文件
存放在 resources\js\assets下
