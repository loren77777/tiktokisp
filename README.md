# 搭建任意地区TikTok专线节点，免拔卡观看TikTok，双isp节点搭建，节点中转提速，寻找纯净IP，解决ip与DNS位置不一致问题whoer
[教程地址](https://youtu.be/du1G5dG1qPQ)
## 流量中转平台推荐： https://g.m123.org
###### GIA线路VPS推荐： https://d.m123.org
###### AT&T高质量住宅IP推荐： https://v.m123.org
###### 相关教程：
###### 专线中转教程：https://youtu.be/gTfOYuU-29U
###### 零基础节点搭建：https://youtu.be/SpxTFes1B8U

## 相关指令
###### 查询IP信息：https://ipinfo.io
###### ip欺诈值查询：https://scamalytics.com/ip
###### 国家字母代码：https://zh.wikipedia.org/wiki/ISO_3166-1
###### 搜索任意国家：https://www.shodan.io/search/facet?facet=isp&query=http.html%3Aassets%2Fqs%2Fqs.min.js+country%3A
###### 搭建X-UI：bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
###### 专线中转：https://g.880805.xyz
###### 国家公共DNS：https://public-dns.info/#countries

## Xray模板-解决DNS与IP不一致问题
```
{
  "dns": {"servers": ["1.1.1.1"]},
  "api": {
    "services": [
      "HandlerService",
      "LoggerService",
      "StatsService"
    ],
    "tag": "api"
  },
  "inbounds": [
    {
      "listen": "127.0.0.1",
      "port": 62789,
      "protocol": "dokodemo-door",
      "settings": {
        "address": "127.0.0.1"
      },
      "tag": "api"
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {"domainStrategy": "ForceIP"}
    },
    {
      "protocol": "blackhole",
      "settings": {},
      "tag": "blocked"
    }
  ],
  "policy": {
    "system": {
      "statsInboundDownlink": true,
      "statsInboundUplink": true
    }
  },
  "routing": {
    "rules": [
      {
        "inboundTag": [
          "api"
        ],
        "outboundTag": "api",
        "type": "field"
      },
      {
        "ip": [
          "geoip:private"
        ],
        "outboundTag": "blocked",
        "type": "field"
      },
      {
        "outboundTag": "blocked",
        "protocol": [
          "bittorrent"
        ],
        "type": "field"
      }
    ]
  },
  "stats": {}
}
```
