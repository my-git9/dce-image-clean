## 使用说明
```bash
Usage: $0 <options> <arguments>
    -a     Action: list|ls|clean|del|delete, Default list
    -h     Registry Host: e.g. "http://127.0.0.1"
    -u     Registry Authorization: e.g. "admin:password"
    -p     Tag Policy:
           e.g.
               count=5 -- Default. Cleanup the digest and keep 5
               days=7  -- Cleanup the digest if it is generated 7 days ago
    -d     Enable debug mode
    -r     Specify the mirror name and then specified -n is invalid
    -n     Define PREFIX namespaces match to delete
Example:
    $0 -h "http://127.0.0.1" -u "admin:password"
    $0 -h "http://127.0.0.1" -u "admin:password" -p "count=5" -d
    $0 -h "http://127.0.0.1" -u "admin:password" -p "days=7"
    $0 -h "http://127.0.0.1" -u "admin:password" -n abcd
    $0 -h "http://127.0.0.1" -u "admin:password" -r "daocloud/dao-2048"
```

示例
查看镜像空间 dx-insight 下面镜像和tag，主要是这个功能需要，
此处加了 -n ，不加的话，要扫描整个 registry ，需要花费一定的时间，没有加 -d ，默认没有输出， 需要的话，可以加上，以免误以为程序卡死了
```bash
[root@dce-10-23-20-155 test]# sh registry.sh -h "http://10.23.114.26" -u "admin:changeme" -n "dx-insight"
Image                                                                  Tag
------------------------------------------------------------------------------------------
dx-insight/dxi-ui                                                      3
dx-insight/dxi-controller                                              3
dx-insight/dxi-proxy                                                   2
dx-insight/thanos                                                      1
dx-insight/prometheus-operator                                         1
dx-insight/prometheus-config-reloader                                  1
dx-insight/prometheus                                                  1
dx-insight/node-exporter                                               1
dx-insight/kube-state-metrics                                          1
dx-insight/grafana                                                     1
dx-insight/event-exporter                                              1
dx-insight/dxi-ui-proxy                                                1
dx-insight/dx-insight-stolon                                           1
dx-insight/dxi-metering-controller                                     1
dx-insight/dx-arch-stolon                                              1
dx-insight/configmap-reload                                            1
dx-insight/busybox                                                     1
dx-insight/alertmanager                                                1
```

查看具体镜像的 tag，dce界面上也可以看，也可以用脚本看，此处参数换成  -r 来进行处理
```bash
[root@dce-10-23-20-155 test]# sh registry.sh -h "http://10.23.114.26" -u "admin:changeme" -r "dx-insight/dxi-ui"
Image                                                                  Tag                   Created
--------------------------------------------------------------------------------------------------------------
dx-insight/dxi-ui                                                      1.3.4-10632          2021-04-07-00-01
dx-insight/dxi-ui                                                      1.3.5-10810          2021-06-25-06-02
dx-insight/dxi-ui                                                      1.4.0-10171          2021-11-17-06-16
```
本脚本原有功能未变动，如果需要删除，需要添加一个参数即可
> 默认 -a 是 list 
> 需要删除掉的话， -a 指定 'clean|del|delete' 即可。其他参数根据需要填写。
```bash
sh registry.sh -h "http://10.23.114.26" -u "admin:changeme"  -a 'del'
```

