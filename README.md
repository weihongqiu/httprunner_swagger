@[toc]
#### 背景
```
鉴于大多数互联网公司均采用java作为后台开发语言，且习惯使用Swagger插件自动生成接口文档；本项目开发依赖此文档完成接口测试。
```
#### 需求
- 为什么要做接口测试
```
受自动化测试分层思想影响：UI自动化投入成本、维护成本大，收益小，
而当下测试人员coding能力有限，那么处于中间层的接口测试战略位置尤为重要；
1、更快实现接口自动化测试，更早加入持续集成；
2、通过定制触发器实时监控生产接口响应状况；
3、后端性能测试更是离不开接口测试的基础。
```
- 如何开展接口测试
```
首先需要了解接口协议，明白接口的组成以及请求和响应过程；
再者需要知道接口测试的影响范围，前端功能测试并不是重复工作；
最后需要清楚业务规则及接口的业务实现逻辑，才能更好的服务接口测试。
```
- 如何才能减去反复的手工活动？
```
做接口测试时，需要组装接口请求url及入参，对着接口文档和接口测试工具无限制的ctrl+c / ctrl+v？

首推自动化技术!

推荐接口测试工具：jmeter/httprunner/postman/rf，不排除其他框架，往着DDT的方向考虑;
接口测试工具原理：都是通过脚本实现模拟客户端向服务端发起请求，然后校验服务器返回数据的过程。
```
#### 实现一
```
python编写脚本对swagger接口文档返回的josn数据对象进行解析，提取接口信息，
按规则写入excel组成测试用例，excel可以提供给jmeter实现数据驱动完成接口自动化测试。
```
#### 实现二
```
引入大疆httprunner框架，同样是通过swagger接口文档生成的json格式的数据文件
<亦可通过charles抓包工具导出har文件，再通过har2case转换json测试用例>，可以直接通过CLI执行；
```
#### 实现三
```
既然已知swagger接口文档并且能解析数据形成excel或者json格式的测试用例，
那么也可以结合python/java等开发语言集合单元测试框架搭建自动化测试框架。
```
#### 项目结构说明：
- logs：存放脚本执行日志
- properties：存放配置信息
- swagger：存放生成json测试用例文件
- swaggerLib：解析swagger接口文档脚本
- utils：封装工具包
- common：
- - dir_config.py：为项目拼接路径配置模块