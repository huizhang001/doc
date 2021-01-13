---
title: easyswoole安装教程
meta:
  - name: description
    content: easyswoole安装教程
  - name: keywords
    content: easyswoole安装教程|swoole框架安装教程
---


# 框架安装

- [GitHub](https://github.com/easy-swoole/easyswoole)  喜欢记得给我们点个 ***star***

::: danger 
注意事项，请看完再进行安装
:::

- 框架使用 `Composer` 作为依赖管理工具，在开始安装框架前，请确保已经按上一章节的要求配置好环境并安装好了 `Composer` 工具
- 关于 `Composer` 的安装可以参照 [Composer中国全量镜像](https://pkg.phpcomposer.com/#how-to-install-composer) 的安装教程
- 目前推荐的镜像为阿里云或者梯子拉取源站
- 在安装过程中，会释放框架的文件到项目目录，请保证项目目录有可写入权限
- 安装完成之后，不会自动生成 `App` 目录，请自行根据 `Hello World` 章节配置


## 框架更新说明(安装之前必看)

- [更新说明](/Update/main.md)


## 切换阿里云镜像
````
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
````

删除镜像
```
composer config -g --unset repos.packagist
```

## Composer 安装

按下面的步骤进行手动安装

```bash
composer require easyswoole/easyswoole=3.x
php vendor/easyswoole/easyswoole/bin/easyswoole install
```


或者
```bash
composer require easyswoole/easyswoole=3.x
php vendor/bin/easyswoole install
```
如果执行成功，则会有如下界面出现
```bash
  php vendor/easyswoole/easyswoole/bin/easyswoole install
  ______                          _____                              _        
 |  ____|                        / ____|                            | |       
 | |__      __ _   ___   _   _  | (___   __      __   ___     ___   | |   ___ 
 |  __|    / _` | / __| | | | |  \___ \  \ \ /\ / /  / _ \   / _ \  | |  / _ \
 | |____  | (_| | \__ \ | |_| |  ____) |  \ V  V /  | (_) | | (_) | | | |  __/
 |______|  \__,_| |___/  \__, | |_____/    \_/\_/    \___/   \___/  |_|  \___|
                          __/ |                                                
                         |___/                                                
  EasySwooleEvent.php has already existed. do you want to replace it? [ Y/N (default) ] : n
  index.php has already existed. do you want to replace it? [ Y/N (default) ] : n
  dev.php has already existed. do you want to replace it? [ Y/N (default) ] : n
  produce.php has already existed. do you want to replace it? [ Y/N (default) ] : n
```
::: danger 
新版安装注意事项
:::

- 新版的 `EasySwoole` 安装会默认提供 `App` 命名空间，还有 `Index` 控制器
- 在这里面需要填写 `n`，不需要覆盖，已经有的 `EasySwooleEvent.php、index.php、dev.php、produce.php`
- 当提示 `exec` 函数被禁用时，请自己手动执行 `composer dump-autoload` 命令更新命名空间

### 安装报错
当执行安装脚本，出现类似以下错误时：
```
dir=$(cd "${0%[/\\]*}" > /dev/null; cd '../easyswoole/easyswoole/bin' && pwd)

if [ -d /proc/cygdrive ]; then
    case $(which php) in
        $(readlink -n /proc/cygdrive)/*)
            # We are in Cygwin using Windows php, so the path must be translated
            dir=$(cygpath -m "$dir");
            ;;
    esac
fi

"${dir}/easyswoole" "$@"
```

请检查环境是否为宝塔等其他集成面板，或者是 `php.ini` 配置项中禁用了 ```symlink``` 与 ```readlink``` 函数，如果禁用了，请关闭这两个函数的禁用，并删除vender目录，然后重新执行 ```composer require``` 或者是 ```composer install``` 或者是 ```composer update```.

如果取消了函数禁用并且删除`vendor`重新`composer`,依旧出现以上错误时,大概率是因为虚拟机等权限原因导致软链接失效.可使用`php vendor/easyswoole/easyswoole/bin/easyswoole`进行开发.或者直接修改`easyswoole`文件,引入`vendor/easyswoole/easyswoole/bin/easyswoole`.

## 启动框架

中途没有报错的话，执行：
```bash
# 启动框架
php easyswoole server start
```
此时可以访问 `http://localhost:9501` 就看到框架的欢迎页面，表示框架已经安装成功

### 可能的问题
- not controller class match
   - `composer.json` 注册 `App` 这个名称空间了吗？
   - 执行过 ```composer dump-autoload``` 了吗？
   - 存在 `Index` 控制器，但是文件大小写、路径都对了吗？

- task socket listen fail
   - 注意，在部分环境下，例如 `win10` 的 `docker` 环境中，不可把虚拟机共享目录作为 `EasySwoole` 的 `Temp` 目录，否则会因为权限不足无法创建 `socket`，产生报错：`listen xxxxxx.sock fail`，为此可以手动在 `dev.php` 配置文件里把 `Temp` 目录改为其他路径即可，如：`'/Tmp'`


## 其他

- QQ 交流群
    - VIP 群 579434607 （本群需要付费599元）
    - EasySwoole 官方一群 633921431(已满)
    - EasySwoole 官方二群 709134628(已满)
    - EasySwoole 官方三群 932625047(已满)
    - EasySwoole 官方四群 779897753(已满)
    - EasySwoole 官方五群 853946743
    
- 商业支持：
    - QQ 291323003
    - EMAIL admin@fosuss.com
        
- 作者微信

     ![](/Images/authWx.png)
    
<script>
        if(localStorage.getItem('isNew') != 1){
            localStorage.setItem('isNew',1);
            layer.confirm('是否给 EasySwoole 点个赞',{offset:'c'},function (index) {
                 layer.msg('感谢您的支持',{offset:'c'});
                     setTimeout(function () {
                         window.open('https://github.com/easy-swoole/easyswoole');
                  },1500);
             });              
        }
</script>
