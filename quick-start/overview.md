---
description: 快速入门
---

### 创建文件

```
package main

import (
	"context"

	"github.com/go-spring/spring-boot"
	_ "github.com/go-spring/starter-echo"
)

func init() {
	SpringBoot.RegisterBean(new(Echo)).Init(func(e *Echo) {
		SpringBoot.GetBinding("/", e.Call)
	})
}

type Echo struct {
	GoPath string `value:"${GOPATH}"`
}

type request struct {
}

func (e *Echo) Call(ctx context.Context, req *request) string {
	return e.GoPath
}

func main() {
	SpringBoot.RunApplication()
}
```

### 启动程序

```
go run main.go
```

控制台输入 `curl http://127.0.0.1:8080` 或浏览器访问,得到如下结果代表程序运行成功

```
{"code":200,"msg":"SUCCESS","data":"/Users/didi/go"}
```