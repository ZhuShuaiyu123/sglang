# MiniMax-H3 SGLang 备份（H200-017）

本仓库是本机 `/kwkj-k8s/zsy/MiniMax-H3/sglang` 的**可恢复代码备份**，用于环境被改坏后把脚本/源码/配置拉回来。

## 上传了什么

- 启动脚本、`public_api_server.py`、`serve_*.yaml`、`sparse/`、`sglang-src/` 等代码与配置
- `requirements-freeze.txt`：当时 venv 的 pip 包列表（便于重建）

## 没有上传什么（太大 / 不该进 Git）

| 路径 | 原因 |
|------|------|
| `.venv/` | ~17GB，用 freeze 重建 |
| `fused/` | ~309GB 融合权重 |
| `outputs/` / `logs/` | 运行产物 |
| `benchmark_turbo/` 大结果 | 体积过大 |
| `*.safetensors` / `*.pt` | 权重与 LoRA |

模型权重仍在机器本地（如 `/kwkj-k8s/SQL/Minimax-h3` 或 `/kwkj-k8s/zsy/MiniMax-H3`）。

## 从 Git 恢复（简版）

```bash
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890
cd /kwkj-k8s/zsy/MiniMax-H3
# 若目录已坏：先备份再 clone
git clone https://github.com/ZhuShuaiyu123/sglang.git sglang-restore
cd sglang-restore
python3 -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install -r requirements-freeze.txt
# 再按本机 env.sh / serve 脚本拉起服务
```

## 拓扑备忘

- FL2VA：4 卡 → `30010`
- REF2VA：4 卡 → `30110`
- Public API：`7880`
- 启动：`bash start_lora_fl2va_ref2va_8gpu.sh`
