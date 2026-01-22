---
name: muc-recommend
description: 群推荐命令处理工具。用于处理 vmtool 群推荐命令，支持两种操作：(1) 取消群推荐 - 修改现有命令将推荐状态从 1 改为 0；(2) 增加群推荐 - 将群 ID 转换为完整的推荐命令。使用场景包括：当用户需要修改群推荐状态时、当用户需要批量生成群推荐命令时、处理群推荐相关的 vmtool 命令时。
---

# MUC Recommend

## 概览

本技能用于处理群推荐相关的 vmtool 命令，支持两种主要操作：

1. **取消群推荐** - 修改现有 vmtool 命令，将推荐状态参数从 `1` 改为 `0`
2. **增加群推荐** - 将群 ID 列表转换为完整的 vmtool 命令

## 核心模板

**vmtool 命令模板：**
```bash
vmtool -x 3 --action getInstances --className im.youni.muc.remote.LbsRoomRecommendServiceImpl --express 'instances[0].saveOrUpdateLbsRoom({群ID}L,"","","",0,{推荐状态},2,4,0,null,null)'
```

其中：
- `{群ID}`: 群的 ID，需要添加 `L` 后缀表示长整型
- `{推荐状态}`: `1` 表示启用推荐，`0` 表示取消推荐

## 操作类型

### 取消群推荐

用户提供一个现有的 vmtool 推荐命令，需要将推荐状态从 `1` 改为 `0`。

**识别特征：**
- 输入为完整的 vmtool 命令
- 命令中包含 `saveOrUpdateLbsRoom(...)` 调用
- 用户明确表示要"取消推荐"

**处理方式：**
1. 保持命令其他部分不变
2. 将推荐状态参数（第6个参数）从 `1` 改为 `0`

**示例：**
```
# 输入
vmtool -x 3 --action getInstances --className im.youni.muc.remote.LbsRoomRecommendServiceImpl --express 'instances[0].saveOrUpdateLbsRoom(112233L,"","","",0,1,2,4,0,null,null)'

# 输出
vmtool -x 3 --action getInstances --className im.youni.muc.remote.LbsRoomRecommendServiceImpl --express 'instances[0].saveOrUpdateLbsRoom(112233L,"","","",0,0,2,4,0,null,null)'
```

### 增加群推荐

用户提供一组群 ID（每行一个），需要为每个群生成完整的 vmtool 推荐命令。

**识别特征：**
- 输入为群 ID 列表（数字，每行一个）
- 用户明确表示要"增加推荐"

**处理方式：**
1. 读取每一行的群 ID
2. 为每个群 ID 生成完整的 vmtool 命令
3. 推荐状态设置为 `1`
4. 确保群 ID 后添加 `L` 后缀

**示例：**
```
# 输入
199293118452046
102246869984064

# 输出
vmtool -x 3 --action getInstances --className im.youni.muc.remote.LbsRoomRecommendServiceImpl --express 'instances[0].saveOrUpdateLbsRoom(199293118452046L,"","","",0,1,2,4,0,null,null)'
vmtool -x 3 --action getInstances --className im.youni.muc.remote.LbsRoomRecommendServiceImpl --express 'instances[0].saveOrUpdateLbsRoom(102246869984064L,"","","",0,1,2,4,0,null,null)'
```

## 处理流程

1. **识别操作类型**
   - 如果输入是完整的 vmtool 命令 → 取消群推荐
   - 如果输入是群 ID 列表 → 增加群推荐

2. **执行处理**
   - 取消推荐：修改状态参数 `0` → `0`，其他内容保持不变
   - 增加推荐：为每个 ID 生成命令，状态设置为 `1`

3. **核对准确性**
   - 确认所有参数格式正确
   - 确认群 ID 的 `L` 后缀存在
   - 确认推荐状态正确（取消为 `0`，增加为 `1`）
   - 确保所有输入的群都生成了对应的命令

## 注意事项

- **必须**准确无误地处理，任何参数错误都可能导致操作失败
- 处理完成后需**核对**每一项内容的准确性
- 群 ID 后必须添加 `L` 后缀表示长整型
- 推荐状态位于 `saveOrUpdateLbsRoom` 的第6个参数位置