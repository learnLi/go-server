# go-server

> 目录结构

- config 配置文件
- controller 控制层
- server 服务层，操作数据库，给控制层提供数据
- forms 字段验证的struct
- global 定义全局变量
- initialize 服务初始化
- logs 日志存储
- middlewares 中间件
- Response 统一封装response
- router 路由
- utils 工具集合
- setting-dev.yaml 配置文件
- main.go 服务启动文件

> 初始化mod

```shell
go mod init go-server
```

> 安装gin

```shell
go get -u github.com/gin-gonic/gin
```

> 编写一个基础gin程序

```
package main

import "github.com/gin-gonic/gin"

func main() {
	r := gin.Default()

	r.GET("/ping", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "pong",
		})
	})

	_ = r.Run() // 监听并在 0.0.0.0:8080 上启动服务
}
```

> 使用Viper配置管理

---
【Viper】适用于go应用程序的配置解决方案。

1. 设置默认值。
2. 用JSON、TOML、YAML、HCL、EnvFile和java properties格式的配置文件读取配置信息
3. 实时监控和重新读取配置文件（可选）
4. 从环境变量中取值
5. 从远程配置系统（etcd|Consul）读取并监控配置变化
6. 从命令行参数读取配置
7. 从buffer读取配置
8. 显示配置值

> 安装Viper

```shell
go get github.com/spf13/viper
```

> 定义配置对应的结构体

在config目录下创建config.go 并创建配置对应的结构体

```go
package config

type ServerConfig struct {
   Name        string      `mapstructure:"name"`
   Port        int         `mapstructure:"port"`
   Mysqlinfo   MysqlConfig `mapstructure:"mysql"`
   RedisInfo   RedisConfig `mapstructure:"redis"`
   LogsAddress string      `mapstructure:"logsAddress"`
}

type MysqlConfig struct {
   Host string `mapstructure:"host"`
   Port int    `mapstructure:"port"`
   Name string    `mapstructure:"name"`
   Password string    `mapstructure:"password"`
   DBName string    `mapstructure:"dbName"`
}

type RedisConfig struct {
   Host string `mapstructure:"host"`
   Port int    `mapstructure:"port"`
}

```



