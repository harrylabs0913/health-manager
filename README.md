# Health Manager

> 智能健康数据管理助手，让健康管理更简单

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-green.svg)](https://github.com/harrylabs0913/health-manager)
[![Clawhub](https://img.shields.io/badge/clawhub-health--manager-purple.svg)](https://clawhub.com/skills/health-manager)

---

## 项目简介

**Health Manager** 是一个命令行健康数据管理工具，帮助你轻松记录和分析自己的健康数据。无论是血压监测、心率跟踪，还是运动记录和用药管理，Health Manager 都能提供简洁高效的管理体验。

### ✨ 核心价值

- **简化记录** - 一条命令完成数据录入
- **智能分析** - 自动生成趋势分析，识别健康模式
- **个性化报告** - 生成专属健康手册，方便与医生分享
- **贴心提醒** - 用药、监测、运动提醒，养成健康习惯

---

## 快速开始

### 安装

```bash
# 从 Clawhub 安装
clawhub install health-manager

# 或从 GitHub 安装
git clone https://github.com/harrylabs0913/health-manager.git
cd health-manager
npm install
npm run build
```

### 初始化配置

```bash
# 设置个人信息
health config init --name "张三" --age 45 --height 175 --weight 70
```

### 第一次记录

```bash
# 记录血压
health bp add 120 80 --heart-rate 72 --notes "早晨测量"

# 记录运动
health ex add running 30 --steps 5000 --calories 300

# 记录用药
health med add "降压药" "1 片" --unit "片"
```

### 查看数据

```bash
# 查看血压记录
health bp list

# 查看血压趋势
health bp trend 7

# 生成日报
health report daily

# 查看健康状态概览
health status
```

---

## 功能特性

### 📊 健康数据记录

| 数据类型 | 支持字段 | 命令示例 |
|---------|---------|---------|
| 血压 | 收缩压、舒张压、心率、备注 | `health bp add 120 80 --heart-rate 72` |
| 运动 | 类型、时长、步数、卡路里、距离 | `health ex add running 30 --steps 5000` |
| 用药 | 药品名称、剂量、单位、备注 | `health med add "降压药" "1 片"` |

### 📈 趋势分析

- **血压趋势** - 7 天/30 天平均血压、心率统计
- **运动统计** - 按类型、按时长、按步数统计
- **异常检测** - 自动识别异常血压记录

### ⏰ 智能提醒

```bash
# 添加用药提醒
health reminder add medication "08:00" --message "该吃药了"

# 添加血压监测提醒
health reminder add bp_monitor "07:00"

# 查看提醒列表
health reminder list
```

### 📖 报告生成

```bash
# 生成日报
health report daily --output daily.md

# 生成周报
health report weekly --output weekly.md

# 生成健康手册
health report handbook --output handbook.md
```

### 📁 数据管理

```bash
# 导出数据
health data export blood_pressure --format csv --output bp.csv
health data export-all ./backups

# 导入数据
health data import blood_pressure data.csv
health data import exercise data.json

# 查看数据库位置
health data path
```

---

## 完整命令参考

### 血压管理 (`health bp`)

```bash
health bp add <收缩压> <舒张压> [选项]     # 添加血压记录
health bp list [选项]                     # 查看血压记录
health bp trend [天数]                    # 查看血压趋势
health bp abnormal                        # 查看异常记录
```

### 运动管理 (`health ex`)

```bash
health ex add <类型> <时长> [选项]        # 添加运动记录
health ex list [选项]                     # 查看运动记录
health ex stats [天数]                    # 查看运动统计
```

### 用药管理 (`health med`)

```bash
health med add <名称> <剂量> [选项]       # 添加用药记录
health med list [选项]                    # 查看用药记录
health med today                          # 查看今日用药
```

### 报告生成 (`health report`)

```bash
health report daily [日期] [选项]         # 生成日报
health report weekly [日期] [选项]        # 生成周报
health report handbook [选项]             # 生成健康手册
```

### 配置管理 (`health config`)

```bash
health config list                        # 查看所有配置
health config set <键> <值>               # 设置配置项
health config init [选项]                 # 初始化用户配置
```

### 提醒管理 (`health reminder`)

```bash
health reminder list                      # 查看提醒
health reminder add <类型> <时间> [选项]  # 添加提醒
health reminder toggle <ID>               # 切换提醒状态
health reminder init                      # 初始化默认提醒
```

---

## 技术栈

- **运行时**: Node.js 18+
- **语言**: TypeScript 5.0+
- **CLI 框架**: Commander.js
- **数据库**: SQLite (better-sqlite3)
- **数据处理**: date-fns
- **终端美化**: chalk, table

---

## 数据结构

### 血压记录

```typescript
{
  id: number;
  systolic: number;      // 收缩压 (mmHg)
  diastolic: number;     // 舒张压 (mmHg)
  heart_rate?: number;   // 心率 (bpm)
  recorded_at: string;   // 记录时间
  notes?: string;        // 备注
}
```

### 运动记录

```typescript
{
  id: number;
  type: string;              // 运动类型
  duration_minutes: number;  // 时长 (分钟)
  steps?: number;            // 步数
  calories_burned?: number;  // 消耗 (千卡)
  distance_km?: number;      // 距离 (公里)
  recorded_at: string;       // 记录时间
}
```

### 用药记录

```typescript
{
  id: number;
  name: string;        // 药物名称
  dosage: string;      // 剂量
  unit?: string;       // 单位
  taken_at: string;    // 服药时间
  notes?: string;      // 备注
}
```

---

## 血压参考标准

| 分类 | 收缩压 (mmHg) | 舒张压 (mmHg) |
|------|-------------|-------------|
| 正常 | < 120 | < 80 |
| 正常偏高 | 120-129 | < 80 |
| 高血压前期 | 130-139 | 80-89 |
| 高血压 1 级 | 140-159 | 90-99 |
| 高血压 2 级 | ≥ 160 | ≥ 100 |

---

## 数据库位置

默认存储在：`~/.config/health-manager/health.db`

可以通过 `health data path` 命令查看具体路径。

---

## 安全说明

- ✅ 所有数据本地存储，不上传云端
- ✅ 无网络请求，保护隐私
- ✅ 开源代码，可审计
- ✅ npm audit 0 漏洞

---

## 开发指南

```bash
# 克隆仓库
git clone https://github.com/harrylabs0913/health-manager.git
cd health-manager

# 安装依赖
npm install

# 开发模式
npm run dev

# 构建
npm run build

# 运行测试
npm test
```

---

## 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建 Pull Request

---

## 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

---

## 联系方式

- 项目主页：https://github.com/harrylabs0913/health-manager
- 问题反馈：https://github.com/harrylabs0913/health-manager/issues
- Clawhub: https://clawhub.com/skills/health-manager
