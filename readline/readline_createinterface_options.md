<!-- YAML
added: v0.1.98
changes:
  - version: v8.3.0, 6.11.4
    pr-url: https://github.com/nodejs/node/pull/13497
    description: Remove max limit of `crlfDelay` option.
  - version: v6.6.0
    pr-url: https://github.com/nodejs/node/pull/8109
    description: The `crlfDelay` option is supported now.
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/7125
    description: The `prompt` option is supported now.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/6352
    description: The `historySize` option can be `0` now.
-->

* `options` {Object}
  * `input` {stream.Readable} 要监听的[可读流][Readable]。此选项是必需的。
  * `output` {stream.Writable} 将逐行读取数据写入的[可写流][Writable]。
  * `completer` {Function} 用于 Tab 自动补全的可选函数。
  * `terminal` {boolean} 如果 `input` 和 `output` 应该被视为 TTY，并且写入 ANSI/VT100 转义码，则为 `true`。
    **默认值:** 实例化时在 `output` 流上检查 `isTTY`。
  * `historySize` {number} 保留的最大历史记录行数。
    要禁用历史记录，请将此值设置为 `0`。
    仅当用户或内部 `output` 检查将 `terminal` 设置为 `true` 时，此选项才有意义，否则根本不会初始化历史记录缓存机制。
    **默认值:** `30`。
  * `prompt` - 要使用的提示字符串。**默认值:** `'> '`。
  * `crlfDelay` {number} 如果 `\r` 与 `\n` 之间的延迟超过 `crlfDelay` 毫秒，则 `\r` 和 `\n` 将被视为单独的行尾输入。
    `crlfDelay` 将被强制转换为不小于 `100` 的数字。
    可以设置为 `Infinity`, 这种情况下，`\r` 后跟 `\n` 将始终被视为单个换行符（对于使用 `\r\n` 行分隔符的[文件读取][reading files]可能是合理的）。
    **默认值:** `100`。
  * `removeHistoryDuplicates` {boolean} 如果为 `true`, 则当添加到历史列表的新输入行与旧的输入行重复时，将从列表中删除旧行。
    **默认值:** `false`。
  * `escapeCodeTimeout` {number} `readline` 将会等待一个字符的持续时间（当以毫秒为单位读取模糊键序列时，可以使用输入读取到目前为止形成完整的键序列，并且可以采取额外的输入来完成更长的键序列）。
     **默认值:** `500`。

`readline.createInterface()` 方法创建一个新的 `readline.Interface` 实例。

```js
const readline = require('readline');
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});
```

一旦创建了 `readline.Interface` 实例，最常见的用例是监听 `'line'` 事件：

```js
rl.on('line', (line) => {
  console.log(`接收到：${line}`);
});
```

如果此实例的 `terminal` 为 `true`，则若它定义了一个 `output.columns` 属性则 `output` 流会获得最佳兼容性，并且如果或当列发生变化时，`output` 上会触发 `'resize'` 事件（当它是 TTY 时，[`process.stdout`] 会自动执行此操作）。

