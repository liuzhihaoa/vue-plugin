# 同创前端组件封装规范

## 依赖组件协议

组件都应依赖`hatech-web-component`组件，并使用其中提供的`mixins`

```js
import ComponentProtocal from 'hatech-web-component'
const { mixins } = ComponentProtocal
export default {
 	name: 'hatech-web-report',
  mixins: [mixins]
}
```

## 单一职责原则

**组件需要保持专一性，即一个组件只负责一个功能**。组件的功能如果可以拆封成多个功能点，应将每个功能点设计成一个小组件，但不是粒度越小越好，只要将一个组件内的功能和逻辑控制在一个可控的范围内即可

## 大功能组合

当一个组件的功能是由多个小功能组合而成时，应使用多个小功能组件组合而成。这个小组件并不一定要发布到npm，也可以是拆分后放在自己的包内的小组件。

## 参数、数据配置

组件运行过程中的参数，应可由参数传入，且参数类型需要指明参数类型。并进行较验，当不符合要求时，应抛出异常。

组件协议mixins中已经集成注入props
* 当组件数据源为对象时，请使用`data`字段
* 当组件数据源为数组时，请使用`list`字段
* 组件配置信息请通过`config`传入

## 生命周期

组件的生命周期都需要发射相关事件钩子，这个在`hatech-web-component`的`mixins`包中已经提供，只需要按规范注入即可

## 事件传递

组件内需要向外界传递事件、数据时，vue`中用$emit `发射、传递

## 注释、说明

组件中应该有详细的使用说明，并有使用示例、demo

组件中每个**自定义方法**、**参数**，都应有**注释**说明。**特殊、复杂业务等**代码，应**多写注释**说明业务。

## 版本

### 格式

- X 表示主版本号，当 API 的兼容性变化时，X 需递增。
- Y 表示次版本号，当增加功能时(不影响 API 的兼容性)，Y 需递增。
- Z 表示修订号，当做 Bug 修复时(不影响 API 的兼容性)，Z 需递增。

### 递增规则

- X, Y, Z 必须为非负整数，且不得包含前导零，必须按数值递增，如 1.9.0 -> 1.10.0 -> 1.11.0
- 0.Y.Z 的版本号表明软件处于初始开发阶段，意味着` API` 可能不稳定；1.0.0 表明版本已有稳定的 API。
- 当 API 的兼容性变化时，X 必须递增，Y 和 Z 同时设置为 0；当新增功能(不影响 API 的兼容性)或者 API 被标记为 Deprecated 时，Y 必须递增，同时 Z 设置为 0；当进行 bug fix 时，Z 必须递增。
- 先行版本号(Pre-release)意味该版本不稳定，可能存在兼容性问题，其格式为：`X.Y.Z.[a-c][正整数]`，如 1.0.0.a1，1.0.0.b99，1.0.0.c1000。
- 开发版本号常用于 CI-CD，格式为 `X.Y.Z.dev[正整数]`，如 1.0.1.dev4。
- 版本号的排序规则为依次比较主版本号、次版本号和修订号的数值，如 1.0.0 < 1.0.1 < 1.1.1 < 2.0.0；对于先行版本号和开发版本号，有：1.0.0.a100 < 1.0.0，2.1.0.dev3 < 2.1.0；当存在字母时，以 ASCII 的排序来比较，如 1.0.0.a1 < 1.0.0.b1。
- 注意：版本一经发布，不得修改其内容，**任何修改必须在新版本发布！**

### 修饰词

- `alpha`：内部版本
- `beta`：测试版
- `demo`：演示版
- `enhance`：增强版
- `free`：自由版
- `full version`：完整版，即正式版
- `lts`：长期维护版本
- `release`：发行版
- `rc`：即将作为正式版发布
- `standard`：标准版
- `ultimate`：旗舰版
- `upgrade`：升级版