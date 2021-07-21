## cmd

发压命令
```
bin/xbench --config=conf/transfer.json

更多命令参考：script/xbench.sh
```

## 配置文件

```json
{
    "total": 1000000,                   // 请求总量

    // 负载参数：两种模式二选一
    // 负载模式1：
    "rps": 100,                         // 恒定的RPS进行测试
    // 负载模式2：
    "load-schedule": "step",            // 步进增长RPS：发送请求起始500rps，每10s增加100rps，最大到5000rps
    "load-start": 500,                  // 起始RPS
    "load-step": 100,                   // 步进值
    "load-end": 5000,                   // 负载结束值
    "load-step-duration": "10s",        // 在每个梯段需要持续的时间

    // 并发参数：两种模式二选一
    // 并发模式1：
    "concurrency": 50,                  // 恒定并发请求数
    // 并发模式2：
    "concurrency-schedule": "step",     // 并发调度算法
    "concurrency-start": 100,           // 起始并发数
    "concurrency-step": 50,             // 并发数步进值
    "concurrency-end": 300,             // 结束并发数
    "concurrency-step-duration": "10s", // 在每个梯段需要持续的时间

    "tags": {                           // 用户自定义参数
        "benchmark": "contract",        // 压测类型

        // amount: 压测账户初始token数，调用合约消耗token，需要保证有充足的token
        // 每一个并发worker使用一个独立账户发送请求，初始化时从bank给每个账户转入amount
        // amount建议值：amount > (total/concurrency) * fee * 2
        "amount": "100000000",          // 压测账户初始token数

        "contract_account": "XC1111111111111111@xuper", // 合约账户
        "code_path": "./contract/counter.wasm",         // 合约二进制文件的路径

        "module_name":"wasm",           // 合约类型
        "contract_name":"counter",      // 合约名
        "method_name":"increase"        // 合约方法
    },

    "host": "10.117.130.40:36301"       // 处理请求的机器
}
```

## 监控服务

```
部署：prometheus + grafana
配置文件：conf/metric
```