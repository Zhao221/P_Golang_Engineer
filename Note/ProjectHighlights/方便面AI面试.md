# 方便面AI面试

北京鳄梨科技有限公司的智能招聘系统是一种利用AI和SaaS技术赋能招聘流程的系统。这个系统涵盖了三大核心服务模块：AI视频面试、ATS智能招聘管理系统和直播招聘。

AI视频面试是一种通过AI技术对面试视频进行影像和文本分析的方式。这种方式适用于大规模岗位的招聘，它可以自动化评估面试者的素质，降低人力筛选的成本，提高客观决策效率。同时，AI视频面试还能让面试者更好地展示自己的能力和特点，提高投递和匹配效率。

ATS智能招聘管理系统则是一种针对大规模岗位的招聘管理系统。它可以通过对面试视频等内容的分析，产生大量数据，对投招行为及人才资质进行更好的判断。这种系统还可以帮助企业更好地管理求职者资源，建立人才私域，形成数据壁垒和行业洞见，灵活地根据需求对智能化流程进行优化。

直播招聘则是一种新的招聘方式，它通过在线直播的形式进行招聘，让企业和求职者在不同的时空下进行互动，更好地匹配需求。

总的来说，北京鳄梨科技有限公司的智能招聘系统是一种利用先进技术提高招聘效率和精度的方式。它涵盖了多种服务模块，可以满足不同类型和规模的招聘需求，并灵活地根据需求进行优化。

北京鳄梨科技有限公司的ATS智能招聘系统是一款基于人工智能技术的招聘管理工具，旨在帮助企业实现招聘流程的自动化、智能化和高效化。以下是关于该系统的详细介绍：

一、系统概述

ATS智能招聘系统是鳄梨科技的核心产品之一，通过整合多种招聘资源和渠道，提供一站式的招聘解决方案。该系统可以自动化管理招聘流程，包括职位发布、简历筛选、面试安排、候选人管理、录用通知等环节，大大提高了招聘效率和准确性。

二、主要功能

1. 职位发布：企业可以在ATS智能招聘系统中轻松发布职位，系统支持多种职位模板和自定义设置，满足不同职位的需求。同时，系统还可以将职位信息自动同步到多个招聘网站和社交媒体平台，扩大职位曝光度。

2. 简历筛选：ATS智能招聘系统通过自然语言处理和机器学习技术，对收到的简历进行自动筛选和分类。系统可以根据职位要求和关键词，快速识别符合要求的候选人，节省企业大量筛选简历的时间。

3. 面试安排：系统支持在线视频面试和线下面试的安排和管理。企业可以根据候选人的情况和招聘需求，灵活安排面试时间和地点。同时，系统还可以自动发送面试邀请和提醒邮件/短信给候选人，确保面试的顺利进行。

4. 候选人管理：ATS智能招聘系统提供完善的候选人管理功能，包括候选人信息录入、状态更新、标签分类、评价反馈等。企业可以随时了解候选人的最新动态和面试进展，为后续的录用决策提供依据。

5. 录用通知：一旦确定录用候选人，ATS智能招聘系统可以自动生成录用通知书并发送给候选人。系统支持自定义设置录用通知书的模板和内容，满足企业的个性化需求。

三、技术特点

1. 智能化：ATS智能招聘系统采用先进的人工智能技术，包括自然语言处理、机器学习、深度学习等，实现招聘流程的自动化和智能化。系统可以自动学习和优化招聘策略，提高招聘效率和准确性。

2. 数据化：系统提供丰富的数据统计和分析功能，帮助企业了解招聘过程中的关键指标和趋势。企业可以根据数据反馈调整招聘策略，提高招聘效果和质量。

3. 安全性：ATS智能招聘系统注重数据安全和隐私保护。系统采用多重加密和安全防护措施，确保企业和候选人的信息安全。

四、应用场景

ATS智能招聘系统适用于各种规模的企业和招聘场景，包括校招、社招、BPO/RPO、零售门店、互联网等多种大规模招聘业务场景。无论是大型企业还是中小型企业，都可以通过该系统实现招聘流程的自动化和智能化管理。

# 任务调度

```go
func Start() {
    cronTask := task.New("auto_check_compare",
       cron.WithChain(cron.Recover(cron.DefaultLogger),
          cron.DelayIfStillRunning(cron.DefaultLogger),
       ),
       cron.WithSeconds(), // 秒级别

    )
    // 获取未处理的图片
    cronTask.AddJob("*/5 * * * * *", GenCompareToken())
    // 处理一个对比组中只有一个checkKey的第一张图片
    cronTask.AddJob("*/5 * * * * *", GenFirstCompareToken())
    // 将当前图片与上一张图片的信息存储到结构中
    cronTask.AddJob("*/5 * * * * *", GenProcessJob())
    // 进行比较判断图片是否作弊
    cronTask.AddJob("*/5 * * * * *", ComProcessJob())
    cronTask.Start()
    cronTask.Wait()
}
```

这段代码是一个Go语言的函数，名为`Start()`。它使用了一个名为`cronTask`的任务调度器，该调度器可以按照指定的时间间隔执行不同的任务。

下面是代码中的任务调度逻辑：

1. 创建一个`cronTask`任务调度器，使用`task.New()`函数进行初始化，并设置了一些选项，如错误恢复、延迟运行等。
2. 使用`cronTask.AddJob()`方法向任务调度器添加不同的任务，每个任务都有一个时间表达式和相应的函数。时间表达式使用Cron表达式语法，用于确定任务的执行时间间隔。
3. 在代码中添加了四个任务：
   - `GenCompareToken()`函数将会每隔 5 秒执行一次，用于获取未处理的图片。
   - `GenFirstCompareToken()`函数将会每隔 5 秒执行一次，用于处理一个只有一个`checkKey`的对比组中的第一张图片。
   - `GenProcessJob()`函数将会每隔 5 秒执行一次，将当前图片与上一张图片的信息存储到某个结构中。
   - `ComProcessJob()`函数将会每隔 5 秒执行一次，用于进行比较判断图片是否作弊。
4. 最后，调用`cronTask.Start()`方法启动任务调度器，并使用`cronTask.Wait()`方法等待所有任务的完成。

总的来说，这段代码通过使用任务调度器实现了按照指定时间间隔执行不同任务的功能。每个任务都有自己的执行函数，可以根据需要进行修改和扩展。

```go
package task

import (
    "github.com/robfig/cron/v3"
    "jihulab.com/elihr/elilong/warehouse/logger"
    "os"
    "os/signal"
    "syscall"
)

type TaskManager struct {
    *cron.Cron
    Name string
}

func New(name string, opts ...cron.Option) *TaskManager {
    return &TaskManager{
       Cron: cron.New(opts...),
       Name: name,
    }
}

func (task *TaskManager) Wait() {
    ch := make(chan os.Signal, 1)
    signal.Notify(ch, os.Interrupt, os.Kill, syscall.SIGTERM)
    select {
    case sig := <-ch:
       logger.Zap().Infow("task receive signal", "taskName", task.Name, "signal", sig)
       ctx := task.Cron.Stop()
       logger.Zap().Infow("task wait exit", "taskName", task.Name, "signal", sig)
       <-ctx.Done()
       logger.Zap().Infow("task success exit", "taskName", task.Name, "signal", sig)

    }
}
```

```go
package logger

import (
    "context"

    "go.uber.org/zap"
    "go.uber.org/zap/zapcore"
)

const DateTimeFormat = "2006-01-02 15:04:05"

// 原始日志
var zc *zap.Logger

// sugar日志
var z *zap.SugaredLogger

// ZapC 原始日志对象
func ZapC() *zap.Logger {
    return zc
}

// Zap sugar日志对象
func Zap() *zap.SugaredLogger {
    return z
}

// WithContext  从context中取得带request-id的sugar日志对象，必须使用middleware_gin.RequestId()
func WithContext(c context.Context) *zap.SugaredLogger {
    zt := c.Value("zap_trace")
    if zt == nil {
       return z
    }

    if v, ok := zt.(*zap.SugaredLogger); ok {
       return v
    }

    return z
}

// 初始化zap日志
func init() {
    // 是否打印堆栈信息
    stacktraceKey := "stacktrace"
    // if env.InProd() {
    //     stacktraceKey = ""
    // }

    encoderConfig := zapcore.EncoderConfig{
       TimeKey:        "time",
       LevelKey:       "level",
       NameKey:        "logger",
       CallerKey:      "caller",
       MessageKey:     "msg",
       StacktraceKey:  stacktraceKey,
       LineEnding:     zapcore.DefaultLineEnding,
       EncodeLevel:    zapcore.LowercaseLevelEncoder,
       EncodeTime:     zapcore.TimeEncoderOfLayout(DateTimeFormat),
       EncodeDuration: zapcore.SecondsDurationEncoder,
       EncodeCaller:   zapcore.ShortCallerEncoder,
    }

    config := zap.Config{
       Level:       zap.NewAtomicLevelAt(zap.DebugLevel),
       Development: false,
       Sampling: &zap.SamplingConfig{
          Initial:    100,
          Thereafter: 100,
       },
       Encoding:         "json",
       EncoderConfig:    encoderConfig,
       InitialFields:    map[string]interface{}{},
       OutputPaths:      []string{"stdout"},
       ErrorOutputPaths: []string{"stderr"},
    }

    // 构建日志对象
    l, err := config.Build()
    if err != nil {
       panic(err)
    }

    // 原始日志
    zc = l

    // sugar日志
    z = l.Sugar()
}
```