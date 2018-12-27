# Tendermint 部署

> 以部署4节点集群为例

- 样例中包括4个节点需要的公私钥文件：genesis.json，priv_validator_1.json， priv_validator_2.json，priv_validator_3.json， priv_validator_4.json

- chain33 源码地址 [https://github.com/33cn/plugin](https://github.com/33cn/plugin) ，下载并编译生成可执行文件 chain33 和 chain33-cli

- 修改样例中的配置文件 chain33.toml，将两处的 IP 地址替换为所部署节点的 IP

```ini
......
[p2p]
seeds=["10.0.0.1:13802","10.0.0.2:13802","10.0.0.3:13802","10.0.0.4:13802"]
......
[consensus.sub.tendermint]
validatorNodes=["10.0.0.1:46656","10.0.0.2:46656","10.0.0.3:46656","10.0.0.4:46656"]
......
```

- 将可执行文件 chain33 和 chain33-cli，修改后的配置文件 chain33.toml，genesis.json 拷贝一份到4个节点上，将 priv_validator_1.json， priv_validator_2.json，priv_validator_3.json， priv_validator_4.json 分别拷贝到对应的节点上并重命名为 priv_validator.json

- 在4个节点上启动 chain33，顺序不分前后，建议在一分钟内全都启动

```shell
./chain33 -f chain33.toml
```

- 在一个节点上使用 chain33-cli 查看区块链状态

```shell
#查看该节点是否与其他节点同步
$ ./chain33-cli net is_sync
true

#查看各个节点的信息
$ ./chain33-cli net peer_info
{
    "peers": [
        {
            "addr": "172.18.0.2",
            "port": 13802,
            "name": "0210c1c09b0d61e41d819e28dcbf1148ebae5fb12a8066a9064e7e1c2346432c91",
            "mempoolSize": 100,
            "self": false,
            "header": {
                "version": 0,
                "parentHash": "0x38e72824d7eb1e147ec5b45f281746f934d152d3f1c04d165b9aa326d7cf407d",
                "txHash": "0xfc26ee8f9aab9362e3f6b6289dad94111eedf9278972a61fcfa5a0aae471d3bf",
                "stateHash": "0x88f0b06df8cd2cd6da81e1580e6f179128e42aa8c66e2dba9c38af3e18f9fa44",
                "height": 52510,
                "blockTime": 1545876177,
                "txCount": 101,
                "hash": "0x808a985f4fa63922c96fb68d896a840a637bbf94655c2eccacb876f5a07849af",
                "difficulty": 0
            }
        },
        {
            "addr": "172.18.0.3",
            "port": 13802,
            "name": "03e8c670f6641e2cc73d149610fd81ffb94c20b83e9428bd61f834adcbf33b3927",
            "mempoolSize": 100,
            "self": false,
            "header": {
                "version": 0,
                "parentHash": "0x38e72824d7eb1e147ec5b45f281746f934d152d3f1c04d165b9aa326d7cf407d",
                "txHash": "0xfc26ee8f9aab9362e3f6b6289dad94111eedf9278972a61fcfa5a0aae471d3bf",
                "stateHash": "0x88f0b06df8cd2cd6da81e1580e6f179128e42aa8c66e2dba9c38af3e18f9fa44",
                "height": 52510,
                "blockTime": 1545876177,
                "txCount": 101,
                "hash": "0x808a985f4fa63922c96fb68d896a840a637bbf94655c2eccacb876f5a07849af",
                "difficulty": 0
            }
        },
        {
            "addr": "172.18.0.4",
            "port": 13802,
            "name": "03a4f80a2d73f999b44e3b1137676e00e5eb1357ce22e9a296b5032cf1d128e0dc",
            "mempoolSize": 100,
            "self": false,
            "header": {
                "version": 0,
                "parentHash": "0x38e72824d7eb1e147ec5b45f281746f934d152d3f1c04d165b9aa326d7cf407d",
                "txHash": "0xfc26ee8f9aab9362e3f6b6289dad94111eedf9278972a61fcfa5a0aae471d3bf",
                "stateHash": "0x88f0b06df8cd2cd6da81e1580e6f179128e42aa8c66e2dba9c38af3e18f9fa44",
                "height": 52510,
                "blockTime": 1545876177,
                "txCount": 101,
                "hash": "0x808a985f4fa63922c96fb68d896a840a637bbf94655c2eccacb876f5a07849af",
                "difficulty": 0
            }
        },
        {
            "addr": "172.18.0.5",
            "port": 13802,
            "name": "0382362b8b1d374646f728ae4e93e103f237747ef59a7518117f4c3483cb05a17b",
            "mempoolSize": 100,
            "self": true,
            "header": {
                "version": 0,
                "parentHash": "0x38e72824d7eb1e147ec5b45f281746f934d152d3f1c04d165b9aa326d7cf407d",
                "txHash": "0xfc26ee8f9aab9362e3f6b6289dad94111eedf9278972a61fcfa5a0aae471d3bf",
                "stateHash": "0x88f0b06df8cd2cd6da81e1580e6f179128e42aa8c66e2dba9c38af3e18f9fa44",
                "height": 52510,
                "blockTime": 1545876177,
                "txCount": 101,
                "hash": "0x808a985f4fa63922c96fb68d896a840a637bbf94655c2eccacb876f5a07849af",
                "difficulty": 0
            }
        }
    ]
}
```