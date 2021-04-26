## 基本环境需要

node 10版本以上

webpack 4.26版本以上

#### 为什么要用webpack?

1. 因为浏览器不能识别scss
2. 浏览器不能识别ES6语法，比如import $ from 'jquery' 就无法被识别

chunk打包之后就是bundle.

webpack会把所有的前端资源全部打包生成对应的静态资源

## webpack五个核心概念

#### 1.entry

告诉webpack打包资源从哪个文件开始打包，也就是指明谁是入口文件

#### 2.output

打包后的资源bundles输出到哪里去，以及如何命名

#### 3.loader

本身webpack只能处理js文件，loader让其可以处理其他格式的文件，也就是翻译官