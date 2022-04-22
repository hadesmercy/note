# 整体架构

* 核心组件

  | 组件名    | 组件功能                  | 目录              |
  | --------- | ------------------------- | ----------------- |
  | cloudcore | Cloud部分各功能模块的集合 | kubeedge/cloud    |
  | edgecore  | Cloud部分各功能模块的集合 | kubeedge/edge     |
  | edge_mesh | 服务网格方案              | kubeedge/edgemesh |
  | edge_site | 边缘独立集群方案          | kubeedge/edgesite |
  | mappers   | 物联网协议实现            |                   |
  | keadm     | kubeedge的一键部署        |                   |

  

## cloudcore

位于cloud/cmd/cloudcore/cloudcore.go目录下

```go
func main() {
	command := app.NewCloudCoreCommand()
	logs.InitLogs()
	defer logs.FlushLogs()

	if err := command.Execute(); err != nil {
		os.Exit(1)
	}
}
```

用到了app.NewCloudCoreCommand这个函数，而该函数是对cobra调用的封装

该函数的实现中使用了registerModules()与core.Run()，这两个函数大量使用

### cobra

* 一个用来构建命令行应用

 >Cobra is a library for creating powerful modern CLI applications.
  >
  >Cobra is used in many Go projects such as [Kubernetes](http://kubernetes.io/), [Hugo](https://gohugo.io/), and [Github CLI](https://github.com/cli/cli) to name a few. [This list](https://github.com/spf13/cobra/blob/master/projects_using_cobra.md) contains a more extensive list of projects using Cobra.

* commands、arguments 和 flags

  行为、命令行参数、命令行选项

  ```go
  Run: func(cmd *cobra.Command, args []string) {
      fmt.Println("cobra demo program")
  }
  ```

* 





Cloud-master 10.112.23.134   //更改名字，作为边，用于计算

Cloud-node1 10.112.252.142   //更改名字，作为边，用于计算

Cloud-node2 10.112.237.49//更改名字，用作云端master

node3 10.112.10.86

node4 10.112.0.250

node5 10.112.228.50

node6 10.112.223.176

node7 10.112.151.202



所有主机的用户名和密码都一致

用户名：root

密码：123456
