---
title: 配置日志等级
description: Rancher 中使用以下日志级别：info、debug、trace。
keywords:
  - rancher 2.0中文文档
  - rancher 2.x 中文文档
  - rancher中文
  - rancher 2.0中文
  - rancher2
  - rancher教程
  - rancher中国
  - rancher 2.0
  - rancher2.0 中文教程
  - 常见故障排查
  - 配置日志等级
---

Rancher 中使用以下日志级别：

| 名称                                                           | 描述                               |
| -------------------------------------------------------------- | ---------------------------------- |
| `info`                                                         | 信息等级日志。这是默认的日志级别。 |
| `debug`                                                        | 将输出更多详细日志，用来帮助调试。 |
| `trace`                                                        |
| 输出内部函数里非常详细的消息。这非常冗长，还可能包含敏感信息。 |

## 如何配置日志等级

### 高可用安装

- 配置 debug 级别

  ```
  $ KUBECONFIG=./kube_config_rancher-cluster.yml
  $ kubectl --kubeconfig $KUBECONFIG -n cattle-system get pods -l app=rancher | grep '1/1' | awk '{ print $1 }' | while read rancherpod; do kubectl --kubeconfig $KUBECONFIG -n cattle-system exec $rancherpod -- loglevel --set debug; done
  OK
  OK
  OK
  $ kubectl --kubeconfig $KUBECONFIG -n cattle-system logs -l app=rancher
  ```

- 配置 info 级别

  ```
  $ KUBECONFIG=./kube_config_rancher-cluster.yml
  $ kubectl --kubeconfig $KUBECONFIG -n cattle-system get pods -l app=rancher | grep '1/1' | awk '{ print $1 }' | while read rancherpod; do kubectl --kubeconfig $KUBECONFIG -n cattle-system exec $rancherpod -- loglevel --set info; done
  OK
  OK
  OK
  ```

### 单节点安装

- 配置 debug 级别

  ```
  $ docker exec -ti <container_id> loglevel --set debug
  OK
  $ docker logs -f <container_id>
  ```

- 配置 info 级别

  ```
  $ docker exec -ti <container_id> loglevel --set info
  OK
  ```
