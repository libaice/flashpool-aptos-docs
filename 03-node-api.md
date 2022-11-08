#### 1. 用户资源获取与单个资源查询

> * 所有资源查询
>
>   https://fullnode.testnet.aptoslabs.com/v1/accounts/0x85c30a87fb365137ac507ed2daa316a21f8b1f64bcd28f0adea60f4f8a1e1cc7/resources
>
> * 单个资源查询
>
>   https://fullnode.testnet.aptoslabs.com/v1/accounts/0x85c30a87fb365137ac507ed2daa316a21f8b1f64bcd28f0adea60f4f8a1e1cc7/resource/0x85c30a87fb365137ac507ed2daa316a21f8b1f64bcd28f0adea60f4f8a1e1cc7::message::MessageHolder



#### 2.Event 的查询

查询某个账号在某个合约下的所以Event

>  https://fullnode.testnet.aptoslabs.com/v1/accounts/{address}/events/{event_handle}/{field_name}
>
> 
>
> https://fullnode.testnet.aptoslabs.com/v1/accounts/0x85c30a87fb365137ac507ed2daa316a21f8b1f64bcd28f0adea60f4f8a1e1cc7/events/0x85c30a87fb365137ac507ed2daa316a21f8b1f64bcd28f0adea60f4f8a1e1cc7::message::MessageHolder/message_change_events



#### 3. Simulate 使用

​		POST 请求  URL

​		`https://fullnode.testnet.aptoslabs.com/v1/transactions/simulate`

 	请求体

* Sender 
* sequence_number   通过账号[ get Account API](https://fullnode.testnet.aptoslabs.com/v1/spec#/operations/get_account) 查询得到
* payload 
  * arguments 参数信息
  * type_arguments  类型参数
* signature  public_key需要与Sender的地址进行匹配

```json
{
    "sender": "0x85c30a87fb365137ac507ed2daa316a21f8b1f64bcd28f0adea60f4f8a1e1cc7",
    "sequence_number": "26",
    "max_gas_amount": "100000",
    "gas_unit_price": "100",
    "expiration_timestamp_secs": "32425224034",
    "payload": {
        "type": "entry_function_payload",
        "function": "0x85c30a87fb365137ac507ed2daa316a21f8b1f64bcd28f0adea60f4f8a1e1cc7::message::set_message",
        "arguments": [  "hello,worldweeee"],
        "type_arguments": [
          
        ]
    },
    "signature": {
        "type": "ed25519_signature",
        "public_key": "0x9ca6dfaa2e5138a503dd8dc20553a51e9ab51870b5a82ffc6e868c751569d6d7",
        "signature": "00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"
    }
}
```

* 返回体中包括
  * 用户资源改变(手续费预估, sequence_number 递增)
  * 执行这笔交易打出Event 中的日志情况





#### 4.一个账号的所有交易

https://fullnode.testnet.aptoslabs.com/v1/accounts/0x85c30a87fb365137ac507ed2daa316a21f8b1f64bcd28f0adea60f4f8a1e1cc7/transactions?limit=1

包括所有资源该变量，一笔交易中的参数，Events