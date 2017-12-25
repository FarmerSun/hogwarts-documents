## Collections
|                      CollectionName                         |                            Description                      | 
|:-----------------------------------------------------------:|:----------------------------------------------------------- | 
|  <a href="#course-meta-anchor">**course_meta**</a>          |  *Basic Information of Courses*                             |
|  <a href="#course-meta-anchor">**course_chapter**</a>       |  *Basic Information of Chapters*                            |
|  <a href="#course-meta-anchor">**course_section**</a>       |  *Basic Information of Sections*                            |  
|  <a href="#course-code-anchor">**course_code**</a>          |  *__All__ Course Codes*                                     |
|  <a href="#course-test-anchor">**course_test**</a>          |  *__All__ Course Test Codes*                                | 
|  <a href="#course-document-anchor">**course_document**</a>  |  *__All__ Course Documents*                                 | 
|  <a href="#template-meta-anchor">**template_meta**</a>      |  *Basic Information of Templates, contains `docker images`* | 
|  <a href="#template-code-anchor">**template_code**</a>      |  *Template Codes*                                           | 
|  <a href="#job-meta-anchor">**job_meta**</a>                |  *__All__ User Testcases MetaInformation*                   |
|  <a href="#job-code-anchor">**job_code**</a>                |  *__All__ User Request Codes*                               |


## Collection Structure

### <a name="course-meta-anchor">**course_meta**</a>
|     Filed    |     Type     |                       Description                       |
|:------------:|:------------:|:------------------------------------------------------- |
|  _id         |  `ObjectId`  |  Automatic Generated Id by mongodb                      |
|  name        |  `String`    |  Course Name                                            |
|  description |  `String`    |  Course Description                                     |
#### Example
```json
{
    _id : <ObjectId1>,
    name : "Nodejs 基础教程",
    description : "Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。"
},
{
    _id : <ObjectId2>,
    name : "Express",
    description : "Express 是基于Node.js 平台,快速、开放、极简的 web 开发框架。"
}
```


### <a name="course-chapter-anchor">**course_chapter**</a>
|     Filed    |     Type     |                       Description                       |
|:------------:|:------------:|:------------------------------------------------------- |
|  _id         |  `ObjectId`  |  Automatic Generated Id by mongodb                      |
|  course_id   |  `ObjectId`  |  Certain `course` this `chapter` belongs to             |
|  name        |  `String`    |  Chapter Name                                           |
|  description |  `String`    |  Chapter Description                                    |
#### Example
```json
{
    _id : <ObjectId3>
    course_id : <ObjectId1>        // --> Course Nodejs //
    name : "Chapter 1 入门",
    description : "简单介绍数据类型, 常用API"
},
{
    _id : <ObjectId4>
    course_id : <ObjectId2>        // --> Course Express //
    name : "Chapter 2 Express 设计理念",
    description : "Express 不对 Node.js 已有的特性进行二次抽象，我们只是在它之上扩展了 Web 应用所需的基本功能。"
}
```


### <a name="course-section-anchor">**course_section**</a>
|     Filed    |     Type     |                       Description                       |
|:------------:|:------------:|:------------------------------------------------------- |
|  _id         |  `ObjectId`  |  Automatic Generated Id by mongodb                      |
|  chapter_id  |  `ObjectId`  |  Certain `chapter` this `section` belongs to            |
|  name        |  `String`    |  Section Name                                           |
|  description |  `String`    |  Section Description                                    |
#### Example
```json
{
    _id : <ObjectId5>
    chapter_id : <ObjectId3>        // --> Course Nodejs --> Chapter 1 //
    name : "小节2 - 字符串",
    description : "Nodejs的字符串操作特别强大, 尤其是字符串模板的优雅和舒服, 谁用谁知道"
},
{
    _id : <ObjectId6>
    chapter_id : <ObjectId4>        // --> Course Express --> Chapter 2//
    name : "小节1 - 为什么这样设计",
    description : "我也不知道为啥这样设计"
}
```


### <a name="course-code-anchor">**course_code**</a>
|     Filed    |     Type     |                           Description                           |
|:------------:|:------------:|:--------------------------------------------------------------- |
|  _id         |  `ObjectId`  |  Automatic Generated Id by mongodb                              |
|  section_id  |  `ObjectId`  |  Certain `section` this `file` belongs to                       |
|  name        |  `String`    |  File Name                                                      |
|  type        |  `String`    |  File Type, values `file` or `dir`                              |
|  parent      |  `String`    |  File Location, `where it locates, absolute path`               |
|  data        |  `String`    |  File Contents, `optional`, *only exist if type equals file*    |
#### Example
```json
{
    _id : <ObjectId7>,
    section_id : <ObjectId5>,         // --> Course Nodejs --> Chapter 1 //
    name : "app.js",
    type : "file",
    parent : "/",
    data : "const _ = require('lodash')\nconsole.log(_.repeate('你好呀'), 666)"      // optional, only exist if type equals file
},
{
    _id : <ObjectId8>,
    section_id : <ObjectId6>,        // --> Course Express --> Chapter 2//
    name : "router",
    type : "dir",
    parent : "/app",
}
```


### <a name="course-test-anchor">**course_test**</a>
|     Filed    |     Type     |                       Description                       |
|:------------:|:------------:|:------------------------------------------------------- |
|  _id         |  `ObjectId`  |  Automatic Generated Id by mongodb                      |
|  section_id  |  `ObjectId`  |  Certain `section` this `test` belongs to               |
|  name        |  `String`    |  Test File Name                                         |
|  data        |  `String`    |  Test File Contents                                     |
**Note : Each section `Only` contains one `Single` test file.**
#### Example
```json
{
    _id : <ObjectId9>,
    section_id : <ObjectId5>,        // --> Course Express --> Chapter 2 --> 小节2 - 字符串 //
    name : "app.js",
    data : "const _ = require('lodash')\n\nconsole.log(_.repeate('你好呀'), 666)"      // optional, only exist if type equals `file`
},
{
    _id : <ObjectId10>,
    section_id : <ObjectId6>,        // --> Course Express --> Chapter 2 --> 小节1 - 为什么这样设计 //
    name : "router",
    data : "cosole.log("Hello Express")",
}
```


### <a name="course-document-anchor">course_document</a>
|     Filed    |     Type     |                       Description                       |
|:------------:|:------------:|:------------------------------------------------------- |
|  _id         |  `ObjectId`  |  Automatic Generated Id by mongodb                      |
|  section_id  |  `ObjectId`  |  Certain `section` this `task document` belongs to      |
|  name        |  `String`    |  Task Document Name                                     |
|  data        |  `String`    |  Task Document Contents                                 |
#### Example
```json
{
    _id : <ObjectId11>,
    section_id : <ObjectId5>,        // --> Course Express --> Chapter 2 --> 小节2 - 字符串 //
    name : "task-nodejs-chapter1-section1-string.md",
    data : "const _ = 在终端打印10遍你好呀"      // optional, only exist if type equals `file`
},
{
    _id : <ObjectId12>,
    section_id : <ObjectId6>,        // --> Course Express --> Chapter 2 --> 小节1 - 为什么这样设计 //
    name : "task-express-chapter2-section2-design.md",
    data : "简介express的设计理念",
}
```


### <a name="template-meta-anchor">template_meta</a>
|     Filed    |     Type     |        Description      |
|:------------:|:------------:|:-----------------------:|
|  name        |  `String`    |  课程名字                |
|  description |  `String`    |  课程描述                |
|  chapters    |  `Array`     |  含有哪些小节的数组       |
#### Example
```json
{
    name : "NodeJS Course",
    description : "Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。"
}
```
### <a name="">template-code-anchor</a>
|     Filed    |     Type     |        Description      |
|:------------:|:------------:|:-----------------------:|
|  name        |  `String`    |  课程名字                |
|  description |  `String`    |  课程描述                |
|  chapters    |  `Array`     |  含有哪些小节的数组       |
#### Example
```json
{
    name : "NodeJS Course",
    description : "Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。"
}
```
### <a name="job-meta-anchor">job_meta</a>
|     Filed    |     Type     |        Description      |
|:------------:|:------------:|:-----------------------:|
|  name        |  `String`    |  课程名字                |
|  description |  `String`    |  课程描述                |
|  chapters    |  `Array`     |  含有哪些小节的数组       |
#### Example
```json
{
    name : "NodeJS Course",
    description : "Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。"
}
```
### <a name="job-code-anchor">job_code</a>
|     Filed    |     Type     |        Description      |
|:------------:|:------------:|:-----------------------:|
|  name        |  `String`    |  课程名字                |
|  description |  `String`    |  课程描述                |
|  chapters    |  `Array`     |  含有哪些小节的数组       |
#### Example
```json
{
    name : "NodeJS Course",
    description : "Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。"
}
```