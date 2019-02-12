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

- 在一个节点上使用 chain33-cli 查询和更新共识状态

```shell
#查询该节点的共识状态是否与其他节点同步
$ ./chain33-cli valnode is_sync
true

#查询 Validator 节点的信息
$ ./chain33-cli valnode nodes
[
    {
        "Address": "XfbMKIZWhdzn9vKn62Zni/KsYYA=",
        "PubKey": "Fi9U4x38QIVZj+uLwuYwfZOwQTKV53VTCwHpr4yrMk4=",
        "VotingPower": 10,
        "Accum": -30
    },
    {
        "Address": "f7w5dyWSgEpcJVw6Ue7VxDAEPhc=",
        "PubKey": "WQDL3b+e3UXta4yTN48N3aGPMmxrWJ0RoXKMOYdZmvo=",
        "VotingPower": 10,
        "Accum": 10
    },
    {
        "Address": "uALH3VlbWTF3391375nqvd4cvt8=",
        "PubKey": "oIvYeW6/9YWoN2MXcea2kUNbqiVDmatChpwHfli8R0Y=",
        "VotingPower": 10,
        "Accum": 10
    },
    {
        "Address": "3G84mV3/caiRkaqLFmCn3TckJms=",
        "PubKey": "Z+7MgI4GiMMUxdQ5tou25IHmz4solSpDLKZpcls1Kcc=",
        "VotingPower": 10,
        "Accum": 10
    }
]

#查询共识状态信息，包括 Commit，State，Proposal，Block
$ ./chain33-cli valnode info -t 1
{
    "SeenCommit": {
        "BlockID": {
            "Hash": "onFZX3CHDbc7yX3SXRT4Zvn5q5E="
        },
        "Precommits": [
            {
                "ValidatorAddress": "XfbMKIZWhdzn9vKn62Zni/KsYYA=",
                "Height": 1,
                "Timestamp": 1549952257288655640,
                "Type": 2,
                "BlockID": {
                    "Hash": "onFZX3CHDbc7yX3SXRT4Zvn5q5E="
                },
                "Signature": "pECET6d8YrsQUC9RVc1RaBj/xW84uM01WG86cBy/Yh4uFSAeDBmYeG1uxNtrOtevPMNZE+ydadDIwrBIugzNDA=="
            },
            {},
            {
                "ValidatorAddress": "uALH3VlbWTF3391375nqvd4cvt8=",
                "ValidatorIndex": 2,
                "Height": 1,
                "Timestamp": 1549952257271146959,
                "Type": 2,
                "BlockID": {
                    "Hash": "onFZX3CHDbc7yX3SXRT4Zvn5q5E="
                },
                "Signature": "j/ft+cfJj8ypM5TAqImEJFeJ6tSWSq9lNf8CKbhkW0XEpgBjGK6n4KrfiGMn9GgIEoO42s5e1bluT6L+PMmcBQ=="
            },
            {
                "ValidatorAddress": "3G84mV3/caiRkaqLFmCn3TckJms=",
                "ValidatorIndex": 3,
                "Height": 1,
                "Timestamp": 1549952257236228239,
                "Type": 2,
                "BlockID": {
                    "Hash": "onFZX3CHDbc7yX3SXRT4Zvn5q5E="
                },
                "Signature": "CULL+q7w5Q1B7st1S36EQ5v9kq7Phgqk7c8FrSC7SxX6fhOketGXw++UOEWt6zzI+Jb+oGMEfIkXRlBaFmUkCg=="
            }
        ]
    },
    "LastCommit": {},
    "State": {
        "ChainID": "chain33-Z2cgFj",
        "LastBlockHeight": 1,
        "LastBlockTime": 1549952257152892815,
        "Validators": {
            "Validators": [
                {
                    "Address": "XfbMKIZWhdzn9vKn62Zni/KsYYA=",
                    "PubKey": "Fi9U4x38QIVZj+uLwuYwfZOwQTKV53VTCwHpr4yrMk4=",
                    "VotingPower": 10,
                    "Accum": -20
                },
                {
                    "Address": "f7w5dyWSgEpcJVw6Ue7VxDAEPhc=",
                    "PubKey": "WQDL3b+e3UXta4yTN48N3aGPMmxrWJ0RoXKMOYdZmvo=",
                    "VotingPower": 10,
                    "Accum": -20
                },
                {
                    "Address": "uALH3VlbWTF3391375nqvd4cvt8=",
                    "PubKey": "oIvYeW6/9YWoN2MXcea2kUNbqiVDmatChpwHfli8R0Y=",
                    "VotingPower": 10,
                    "Accum": 20
                },
                {
                    "Address": "3G84mV3/caiRkaqLFmCn3TckJms=",
                    "PubKey": "Z+7MgI4GiMMUxdQ5tou25IHmz4solSpDLKZpcls1Kcc=",
                    "VotingPower": 10,
                    "Accum": 20
                }
            ],
            "Proposer": {
                "Address": "f7w5dyWSgEpcJVw6Ue7VxDAEPhc=",
                "PubKey": "WQDL3b+e3UXta4yTN48N3aGPMmxrWJ0RoXKMOYdZmvo=",
                "VotingPower": 10,
                "Accum": -20
            }
        },
        "LastValidators": {
            "Validators": [
                {
                    "Address": "XfbMKIZWhdzn9vKn62Zni/KsYYA=",
                    "PubKey": "Fi9U4x38QIVZj+uLwuYwfZOwQTKV53VTCwHpr4yrMk4=",
                    "VotingPower": 10,
                    "Accum": -30
                },
                {
                    "Address": "f7w5dyWSgEpcJVw6Ue7VxDAEPhc=",
                    "PubKey": "WQDL3b+e3UXta4yTN48N3aGPMmxrWJ0RoXKMOYdZmvo=",
                    "VotingPower": 10,
                    "Accum": 10
                },
                {
                    "Address": "uALH3VlbWTF3391375nqvd4cvt8=",
                    "PubKey": "oIvYeW6/9YWoN2MXcea2kUNbqiVDmatChpwHfli8R0Y=",
                    "VotingPower": 10,
                    "Accum": 10
                },
                {
                    "Address": "3G84mV3/caiRkaqLFmCn3TckJms=",
                    "PubKey": "Z+7MgI4GiMMUxdQ5tou25IHmz4solSpDLKZpcls1Kcc=",
                    "VotingPower": 10,
                    "Accum": 10
                }
            ],
            "Proposer": {
                "Address": "XfbMKIZWhdzn9vKn62Zni/KsYYA=",
                "PubKey": "Fi9U4x38QIVZj+uLwuYwfZOwQTKV53VTCwHpr4yrMk4=",
                "VotingPower": 10,
                "Accum": -30
            }
        },
        "LastHeightValidatorsChanged": 1,
        "ConsensusParams": {
            "BlockSize": {
                "MaxBytes": 22020096,
                "MaxTxs": 100000,
                "MaxGas": -1
            },
            "TxSize": {
                "MaxBytes": 10240,
                "MaxGas": -1
            },
            "BlockGossip": {
                "BlockPartSizeBytes": 65536
            },
            "EvidenceParams": {
                "MaxAge": 100000
            }
        },
        "LastHeightConsensusParamsChanged": 1
    },
    "Proposal": {
        "height": 1,
        "timestamp": 1549952257153442871,
        "POLRound": -1,
        "POLBlockID": {},
        "signature": "lzakTHOmuIGVjt0nMeGPaOb1pz1OdoUOVccx6x66r88/7+2DrhyQKHjW2nY5gbr7Jo/M8lt201ppwP14y3lfAQ==",
        "blockhash": "onFZX3CHDbc7yX3SXRT4Zvn5q5E="
    },
    "block": {
        "header": {
            "chainID": "chain33-Z2cgFj",
            "height": 1,
            "time": 1549952257152892815,
            "lastBlockID": {},
            "validatorsHash": "blfKcVDClMuaCxN/edFDatBah1dlWB3ITAsIras+DxY=",
            "consensusHash": "/GlQqG9MV+dJNFIoxo0NOSvVUDU="
        },
        "evidence": {},
        "lastCommit": {},
        "proposerAddr": "XfbMKIZWhdzn9vKn62Zni/KsYYA="
    }
}

#删除 Validator 节点
$ ./chain33-cli valnode add -p 162F54E31DFC4085598FEB8BC2E6307D93B0413295E775530B01E9AF8CAB324E -w 0

#增加 Validator 节点，power 值必须少于当前总的 voting power 值的 1/3
$ ./chain33-cli valnode add -p 162F54E31DFC4085598FEB8BC2E6307D93B0413295E775530B01E9AF8CAB324E -w 9
```