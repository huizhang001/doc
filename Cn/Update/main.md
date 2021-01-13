# 框架更新记录
> 框架更新记录仅仅整理自2020年10-24后的记录，其余记录以老版本文档或github记录为准。

## 3.4.2 - 2020-12-22

### 优化

- `task`优化,更加灵活的配置.
- `crontab`优化,避免极端情况下任务不执行.
- `http-dispatcher`优化,更加灵活的注册路由.

## 3.4.1 - 2020-11-18

### 新增

- 增加`SysConst::EXECUTE_COMMAND`,此常量可获取主框架内部所执行的`command`.
- `install`命令函数检查`symlink`和`readlink`。

### 修复

- 修复`worker`异常退出，没有清理`table`信息。

### 移除

- 移除command及bridge中config功,因为非`swoole-table`.

## 3.4.0 - 2020-10-24

与`3.3.x`不兼容，需进行调整.

`3.3.x -> 3.4.x`需要重新执行`php vendor/bin/easyswoole install`.

### 新增

- `Core::getInstance()->runMode();`方法. 可通过此方法修改运行文件,默认`dev`,也可以通过`command`进行修改.

### 变更

- [command](/QuickStart/command.md)命令变更.

- 自定义`command`需进行[调整](https://github.com/easy-swoole/command).

- `config`从`swoole-table`改为`splArray`,用户可自行调整.

- `onRequest`及`afterRequest`全局事件
变更为(`initialize`注册即可):
```php
\EasySwoole\Component\Di::getInstance()->set(\EasySwoole\EasySwoole\SysConst::HTTP_GLOBAL_ON_REQUEST, callback);
\EasySwoole\Component\Di::getInstance()->set(\EasySwoole\EasySwoole\SysConst::HTTP_GLOBAL_AFTER_REQUEST, callback);
```
`callback`为回调函数,注入参数为：
```php
function (\EasySwoole\Http\Request $request, \EasySwoole\Http\Response $response){}
```
`onRequest`事件需要返回`bool`,来决定程序是否继续进行`dispatcher`.

### 移除

- 移除`EasySwooleEvent`中`onRequest`及`afterRequest`全局事件.

- 移除`Core::getInstance()->isDev();`方法.

- 移除`Core::getInstance()->globalInitialize();`,可自行调用`EasySwooleEvent::initialize()`.
