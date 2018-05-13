# 代码规范

## 一、前端代码规范

### Javascript规范

- 使用两个空格代替Tab进行缩进
- 不允许使用分号
- 使用let和const代替var，特别的对于不需要修改的使用const
- 不允许行尾空格
- 不允许连续多行空白行
- 字符串使用单引号
- 组件 props 原子化
        提供默认值
        使用 type 属性校验类型
        使用 props 之前先检查该 prop 是否存在
- 避免 this.$parent
- 谨慎使用 this.$refs
- 无需将 this 赋值给 component 变量
- 调试信息console.log() debugger 使用完及时删除

### Vue命名规范

#### .vue 文件命名规范

- 尽量使用名词
- 放在模块文件夹内
- 大写字母开头

#### vue 方法放置顺序

- components
- props
- data
- created
- mounted
- activited
- update
- beforeRouteUpdate
- metods
- filter
- computed
- watch


#### method 自定义方法命名

- 动宾短语
- ajax方法使用get、post开头，data结尾
- 事件方法以on开头
- init,refresh例外
- 尽量使用简单常见的单词
- 使用驼峰法

### 注释规范

以下情况为必须使用注释的地方：

- 公共组件使用说明
- 各组件中重要函数或者类说明
- 复杂的业务逻辑处理说明
- 特殊情况的代码处理说明,对于代码中特殊用途的变量、存在临界值、函数中使用的hack、使用了某种算法或思路等需要进行注释描述




---

## 二、后端代码规范