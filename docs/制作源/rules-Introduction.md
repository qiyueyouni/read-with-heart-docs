# 规则

## 参数说明

### 系统自带get参数
| 参数名称          | 说明        | 使用场景           | 用例                    |
|:--------------|-----------|:---------------|:----------------------|
| keyword       | 关键词       | 书籍搜索           | `@get{keyword}`       |
| preResHeader1 | 前置请求标头    | 全局可用           | `@get{preResHeader1.xxx}` |
| preRepHeader1 | 前置响应标头    | 全局可用           | `@get{preRepHeader1.xxx}` |
| resHeader     | 请求标头      | 全局可用           | `@get{resHeader.xxx}` |
| repHeader     | 响应标头      | 全局可用           | `@get{repHeader.xxx}` |
| loginRequest  | 登录请求头     | 全局可用           | `@get{loginRequest}`  |
| loginResponse | 登录响应头     | 全局可用           | `@get{loginResponse}` |
| loginCookies  | 登录cookies | 全局可用           | `@get{loginCookies}`  |
| verifyHeader  | 浏览器过盾请求头  | 正文请求           | `@get{verifyHeader}`  |
| verifyCookies | 浏览器过盾cookies | 正文请求        | `@get{verifyCookies}` |
| bookUrl       | 书籍地址      | 章节列表、正文使用      | `@get{bookUrl}`       |
| chapterUrl    | 章节地址      | 正文使用           | `@get{chapterUrl}`    |
| host          | 主地址       | 全局可用           | `@get{host}`          |

**说明：**
- 前置响应标头使用数字标记，用于保存所有的前置请求（如 preResHeader1、preResHeader2...）
- `verifyHeader` 和 `verifyCookies`：正文请求如果有浏览器过盾，会自动加入过盾请求头和cookies，如果为空则会弹出过盾弹窗
- `loginRequest`、`loginResponse`、`loginCookies`：点击登录后会自动保存，可在书源中获取使用

### 系统内置JS函数

除了 App 对象提供的方法外，系统还内置了一些常用的 JavaScript 函数：

| 函数名称 | 说明 | 用例 |
|:---|:---|:---|
| `console.log()` | 打印调试信息 | `console.log('你好世界')` |
| `console.log([])` | 打印数组 | `console.log(['你好', '世界'])` |
| `unicode.decode()` | Unicode 解码 | `let string = "\\u006b"`<br/>`unicode.decode(string)` |

**说明：**
- `console.log()` 等同于 `App.log()`，可以互换使用
- `unicode.decode()` 等同于 `App.unicode.decode()`
- 更多 Native to Javascript 方法请参考[Native to Javascript](../native-to-js.md)文档

### 公共内置请求参数
| 参数名称           | 说明        | 用例                      | 值类型示例                      |
|:---------------|-----------|:------------------------|:---------------------------|
| params         | 请求参数      | `config.params`         |                            |
| engine         | 源引擎类型     | `config.engine`         | xpath、jsonpath             |
| method         | 请求类型      | `config.method`         | POST，GET                   |
| host           | 站点地址      | `config.host`           |                            |
| header         | 请求头       | `config.header`         | 优先级别：正式请求头>浏览器过盾请求头>公共请求头  |
| mode           | 请求模式      | `config.mode`           | http、webview               |
| requestEncode  | 请求编码方式    | `config.requestEncode`  | utf-8、gbk                  |
| responseEncode | 响应编码方式    | `config.responseEncode` | utf-8、gbk                  |
| cookies        | cookies信息 | `config.cookies`        |                            |
| openParams     | 开放参数，可自定义 | `config.openParams`     |                            |
| verifyCode     | 验证码       | `config.verifyCode`     |                            |

### 搜索规则

| 参数名称 | 说明 | 用例               |
|:---|:---|:-----------------|
| keyword | 搜索关键词 | `config.keyword` |
| url | 搜索地址 | `config.url`     |

### 详情规则

### 章节列表规则

| 参数名称   | 说明                             | 用例                                     |
|:---|:---|:---------------------------------------|
| bookUrl   | 章节列表url                       | `config.bookUrl`                       |
| infoUrl   | 书籍信息url                       | 如果书籍详情有规则，会先调用`infoUrl`请求，并获取`bookUrl` |
| bookName  | 书籍名称                         | `config.bookName`                      |
| bookAuthor| 作者                             | `config.bookAuthor`                    |
| url       | 章节列表请求地址                   | `config.url`                           |
| pageIndex | 页码                             | `config.pageIndex`                     |
| pageStart | 起始章节页数（老版本参数不建议使用） | 用于章节规则拼接，如第二章起，标记2                     |

### 正文规则

| 参数名称   | 说明               | 用例                   |
|:---|:---|:---------------------|
| bookUrl   | 章节列表Url         | `config.bookUrl`     |
| bookName  | 书籍名称           | `config.bookName`    |
| bookAuthor| 作者               | `config.bookAuthor`  |
| chapterUrl| 章节详情Url         | `config.chapterUrl`  |
| infoUrl   | 书籍详情Url         | `config.infoUrl`     |
| chapterName| 章节名称         | `config.chapterName` |
| url       | 正文请求地址        | `config.url`         |
| pageIndex | 页码               | `config.pageIndex`   |
| pageStart | 起始章节页数（老版本参数不建议使用） | 用于正文规则拼接，如第二章起，标记2   |
| playUrl   | 如果`playUrl`规则为空，自动获取正文url和正文header | `config.playUrl`     |

### 发现规则

| 参数名称 | 说明             | 用例                 |
|:---|:---|:-------------------|
| url     | 发现请求地址      | `config.url`       |
| pageIndex | 章节页数序列      | `config.pageIndex` |

### 表达式

APP内置了各种常用的表达式，可以进行替换获取和处理操作。

| 参数 | 名称 | 示例 | 说明 |
|:---|:---|:---|:---|
| `${}` | 获取参数 | `${key}` | 支持获取json的子集`${info.name}` |
| `@{}` | 获取参数 | `@{key}` | 等同于`${}` |
| `{{}}` | 运行规则 | `{{}}` |可以运行xpath、jsonpath的规则 |
| `@get{}` | 获取put信息 | `@get{name}` | 可以获取`@put{}`的数据 |
| `@put{}` | 保存信息 | `@put{name, '//*[@src]'}` | 目前只支持前置请求的put |
| `<js></js>` | 运行JS语言 | `<js>App.log('hello!');</js>` | 在标签内可以运行js的语言 |
| `@js:` | JS语言处理 | @js:<br/>let name = '张三';<br/>App.log(name); | 在规则中第一行添加`@js:`表示该规则使用js运行 |
| `@all` | 获取网页所有内容 | `@all` | 不使用任何规则，直接获取网页原文 |
| `##正则表达式#替换字符` | 正则替换 | `##a#b` | 替换一次 |
| `##正则表达式##替换字符` | 正则替换 | `##a##b` | 替换所有 |
| `##正则表达式` | 正则替换 | `##a` | 过滤所有 |
| `##正则表达式#$1` | 正则替换 | `##(*.?)#$1` | 取值，如果有子串，可按照$1\$2\$3...直接取值 |

## URL规则

### 图片URL
有些图片需要增加请求头才能正常加载，可以使用以下方式：

```javascript
// 在图片规则中使用 <js></js> 标签
data.image<js>
return `${data.image}, {
  "header": { 
    "Referer": "https://example.com",
    "User-Agent": "Mozilla/5.0"
  }
}`
</js>
```

### 过盾跨域名获取Cookie
当需要获取非当前主域名的内置浏览器cookie时，需要设置 `domains` 参数：

```json
{
  "domains": [
    "qidian.com",
    "example.com"
  ]
}
```

**说明：** 此配置用于浏览器过盾场景，允许跨域获取指定域名的Cookie信息。
