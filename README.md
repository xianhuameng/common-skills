# common-skills

A collection of useful Claude Code skills for common development tasks.

## Skills

### muc-recommend

群推荐命令处理工具，用于处理 vmtool 群推荐命令。

**功能：**
- 取消群推荐：修改现有命令，将推荐状态从 `1` 改为 `0`
- 增加群推荐：将群 ID 转换为完整的推荐命令

**使用场景：**
- 修改群推荐状态
- 批量生成群推荐命令
- 处理群推荐相关的 vmtool 命令

### project-select

工作区项目导航工具，用于在多个项目之间快速切换。

**功能：**
- 列出工作区中所有项目（按字母顺序排序）
- 快速导航到指定项目目录

**使用场景：**
- 在包含多个子项目的工作区中切换项目
- 快速定位并进入目标项目目录

**工作流程：**
1. 导航到工作区目录
2. 列出所有可用项目
3. 进入用户指定的项目目录

## Installation

1. Clone this repository:
```bash
git clone https://github.com/xianhuameng/common-skills.git
cd common-skills
```

2. Follow the Claude Code skill installation guide:
https://claude.com/blog/how-to-create-skills-key-steps-limitations-and-examples

## License

common-skills is licensed under Apache License v2.0.
