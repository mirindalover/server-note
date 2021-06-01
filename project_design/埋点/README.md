
### 子午线

客户端sdk,可以通过服务端下发上报策略(如根据网络环境，事件类型)，优先上报

服务端：Nginx+Lua+Openresty+LuaJIT

Lua(过滤、消息检查、白名单)->C(解密、解析json)->Kafka()
