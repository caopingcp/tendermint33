# Tendermint 部署

> 以部署4节点集群为例

- 样例中包括4个节点需要的公私钥文件：genesis_file.json，priv_validator_1.json， priv_validator_2.json，priv_validator_3.json， priv_validator_4.json

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

- 将可执行文件 chain33 和 chain33-cli，修改后的配置文件 chain33.toml，genesis_file.json 拷贝一份到4个节点上，将 priv_validator_1.json， priv_validator_2.json，priv_validator_3.json， priv_validator_4.json 分别拷贝到对应的节点上并重命名为 priv_validator.json

- 在4个节点上启动 chain33，顺序不分前后，建议在一分钟内全都启动

```shell
chain33 -f chain33.toml
```