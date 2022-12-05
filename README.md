# go-wiki
golang 相关工具

## 常用工具
### caddy
- caddy是一个性能堪比nginx的web server，其优势是安装和使用简单，只要golang能运行的平台都能快速的安装，并简单的配置就能高效的运行

### drone
- ci工具，搭配gogs使用效果不错，业内也有不少的团队使用 gogs + drone + k8s 搭建完整的cicd服务

### gogs
- 轻量级git服务，gogs可以轻易的部署在golang能运行的所有平台，并且性能比gitlab高很多倍，缺点是功能没有那么全，日常使用足够
开源项目

### kratos
- bilibili开源的一个微服务包，可以直接生成grpc+http代码，并且高度抽象，你可以自由定制成适合自己团队的框架

### ClickHouse
- 日志检索工具

## 好用的包
### golang.org/x/sync/errgroup
- 捕获多个goroutine中的第一个出现的错误
- 示例
```
// 如果需要达到其中一个失败就全部失败的情况，需要使用errgroup.WithContext()方法
eg := errgroup.Group{}
eg.Go(func() error {
// your handler code
})
eg.Go(func() error {
// your handler code
})

err = eg.Wait()
if err != nil {
log.Errorf("failed, err: %v", err)
}
```

### github.com/pkg/errors
- 他可以帮助你包装原始错误，并且携带堆栈信息以及附加其他的调试信息，不建议在包里面使用，而是在业务层使用更合适，
- 示例
```
// service A
return err

// service B
err := A()
if nil != err {
// WithStack, Wrap方法会附加堆栈信息，整个调用栈中应该只使用一次
return errors.WithStack(err)
}

// service C
err := B()
if nil != err {
return errors.WithMessage(err, "error message");
}
```
