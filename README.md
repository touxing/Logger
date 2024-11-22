# Web 浏览器日志记录器

前端的日志记录，一般使用埋点监控系统，比如 sentry。能用埋点系统，还是建议用埋点系统。但是在局域网的场景中，开发工程师又无法远程查看的情况下，记录web日志，分析日志就变得重要了。此项目就是在此背景下诞生的。（用浏览器记录web日志，确实是挺奇怪的行为）


# 使用

## 安装
```shell
pnpm i @hotsuitor/logger
```

## 方法

```ts
interface Logger {
    log(level: LogLevel, message: string): void {}
    debug(message: string) {}
    info(message: string) {}
    warn(message: string) {}
    error(message: string) {}
}
```

在需要记录日志的地方使用

### example

```js
import { Logger } from 'logger'

// 省略其他代码

// 记录错误信息，可以结合 window.addEventlistener('error', () => {})
Logger.error(
    JSON.stringify({
    message: err.message,
    stack: err.stack,
    })
)
```

### example2

```js
window.addEventListener('error', (event) => {
  Logger.error(
    JSON.stringify({
      message: event.message,
      source: event.filename,
      lineno: event.lineno,
      colno: event.colno,
      stack: event.error ? event.error.stack : 'No stack trace available',
    })
  );
});
```