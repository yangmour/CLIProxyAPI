# cli-proxy-api 本地部署配置

## 1.CPA 配置文件 二选一既可使用(config.yaml.bak这个是原版案例)
### 方式1：shell生成config.yaml和新密钥
```shell
#!/bin/bash

# 生成随机 key（Mac/Linux通用）
SK_KEY="sk-cpa-$(LC_CTYPE=C tr -dc 'a-z0-9' </dev/urandom | head -c 32)"
SECRET_KEY="mgt-cpa-$(LC_CTYPE=C tr -dc 'a-z0-9' </dev/urandom | head -c 32)"

cat <<EOF > config.yaml
# CPA 配置 — Cloudflare Tunnel 方案

host: "127.0.0.1"
port: 8317
auth-dir: "~/.cli-proxy-api"
request-retry: 3
quota-exceeded:

switch-project: true
switch-preview-model: true

api-keys:
- "$SK_KEY"

remote-management:
  allow-remote: true
  secret-key: "$SECRET_KEY"

disable-control-panel: false
logging-to-file: true
usage-statistics-enabled: true
logs-max-total-size-mb: 100
EOF

echo "*** --config.yaml-- 已生成 ***"
echo "*** --仅显示一次,请记录你的明文密钥 -- ***"
echo "Claude/API Key: $SK_KEY"
echo "Secret Key: $SECRET_KEY"
```

### 方式二:直接可用的config.yaml配置文件
```shell
# CPA 配置 — Cloudflare Tunnel 方案

host: "0.0.0.0"
port: 8317
auth-dir: "~/.cli-proxy-api"
request-retry: 3
quota-exceeded:

switch-project: true
switch-preview-model: true

api-keys:
- "sk-cpa-lgkbqadxc14n59flqdsvzcbah4l5mc2v"

remote-management:
  allow-remote: true
  secret-key: "mgt-cpa-gr1qybg3xo9dinicgwoo18bnhshnhg3t"

disable-control-panel: false
logging-to-file: true
usage-statistics-enabled: true
logs-max-total-size-mb: 100

```

## 2.启动CPA
```shell
docker compose up -d
```

## 3.浏览器访问网址
http://localhost:8317/management.html

## 账号
4.搭配chatgpt_register.py使用