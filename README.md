# 配置文件

```json
{
    "total": 1000000,                   // 请求总量
    "concurrency": 50,                  // 并发请求数

    // 负载参数
    // 负载模式1：
    "rps": 100,                         // 恒定的RPS进行测试
    // 负载模式2：
    "load-schedule": "step",            // 步进增长RPS：发送请求起始500rps，每10s增加100rps，最大到5000rps
    "load-start": 500,                  // 起始RPS
    "load-step": 100,                   // 步进值
    "load-end": 5000,                   // 负载结束值
    "load-step-duration": "10s",        // 在每个梯段需要持续的时间

    // 并发参数
    "concurrency-schedule": "step",     // 并发调度算法
    "concurrency-start": 100,           // 起始并发数
    "concurrency-step": 50,             // 并发数步进值
    "concurrency-end": 300,             // 结束并发数
    "concurrency-step-duration": "10s", // 在每个梯段需要持续的时间

    "insecure": true,                   // grpc insecure模式
    "call": "pb.Xchain.PostTx",         // 指定调用的方法
    "proto": "./pb/xchain.proto",       // 指定 proto 文件位置
    "import-paths": [                   // 依赖 proto 文件位置
        "./pb/googleapis"
    ],

    "tags": {                              // 用户自定义参数
        "module_name":"wasm",              // 合约类型
        "contract_name":"short_content",   // 合约名
        "method_name":"storeShortContent", // 合约方法
        "length":"256"                     // 短文本内容长度
    },

    "host": "10.117.130.40:36301"          // 处理请求的机器
}
```