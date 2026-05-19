# vue-global-hijack 配置文件说明

## 接口地址

```
https://raw.githubusercontent.com/weizuihou/test/refs/heads/main/config-example.json
```

## 配置结构说明

### 1. 全局开关

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `enabled` | boolean | true | 全局开关，控制所有劫持是否生效 |

### 2. Date 劫持配置

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `Date.offsetMinutes` | number | 83 | 时间偏移分钟数 |

**注意**：Date劫持只要 `enabled=true` 就始终生效，不受时间条件限制。

### 3. 定时器劫持配置

适用于：`setTimeout`, `setInterval`

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `delay` | number | 3000 | 覆盖的延迟/间隔时间（毫秒） |

### 4. 数组过滤方法配置

适用于：`map`, `forEach`, `filter`, `concat`, `slice`, `splice`, `reverse`, `sort`

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `filterCount` | number | 1 | 要过滤掉的元素数量 |
| `filterCondition` | string | "random" | 过滤位置："head"(头部), "tail"(尾部), "random"(随机) |

### 5. 布尔值方法配置

适用于：`some`, `every`, `includes`

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `overrideResult` | boolean | false | 覆盖返回值 |

### 6. Reduce 方法配置

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `overrideResult` | any | 999 | 覆盖返回值（可以是任意类型） |

### 7. 查找方法配置

适用于：`find`

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `overrideResult` | any | null | 覆盖返回值 |

### 8. 索引方法配置

适用于：`findIndex`, `indexOf`, `lastIndexOf`

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `overrideResult` | number | -1 | 覆盖返回值 |

### 9. Join 方法配置

| 字段 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `overrideResult` | string | "hijacked" | 覆盖返回值 |

## 完整配置示例

```json
{
  "enabled": true,
  "Date": {
    "offsetMinutes": 83
  },
  "setTimeout": {
    "delay": 3000
  },
  "setInterval": {
    "delay": 3000
  },
  "map": {
    "filterCount": 1,
    "filterCondition": "random"
  },
  "forEach": {
    "filterCount": 1,
    "filterCondition": "random"
  },
  "filter": {
    "filterCount": 1,
    "filterCondition": "random"
  },
  "concat": {
    "filterCount": 1,
    "filterCondition": "random"
  },
  "slice": {
    "filterCount": 1,
    "filterCondition": "random"
  },
  "splice": {
    "filterCount": 1,
    "filterCondition": "random"
  },
  "reverse": {
    "filterCount": 1,
    "filterCondition": "random"
  },
  "sort": {
    "filterCount": 1,
    "filterCondition": "random"
  },
  "some": {
    "overrideResult": false
  },
  "every": {
    "overrideResult": false
  },
  "includes": {
    "overrideResult": false
  },
  "reduce": {
    "overrideResult": 999
  },
  "find": {
    "overrideResult": null
  },
  "findIndex": {
    "overrideResult": -1
  },
  "indexOf": {
    "overrideResult": -1
  },
  "lastIndexOf": {
    "overrideResult": -1
  },
  "join": {
    "overrideResult": "hijacked"
  }
}
```

## 配置示例

### 示例1：只启用 Date 劫持

```json
{
  "enabled": true,
  "Date": {
    "offsetMinutes": 83
  }
}
```

### 示例2：只启用定时器劫持

```json
{
  "enabled": true,
  "setTimeout": {
    "delay": 3000
  },
  "setInterval": {
    "delay": 5000
  }
}
```

### 示例3：只启用数组过滤

```json
{
  "enabled": true,
  "map": {
    "filterCount": 1,
    "filterCondition": "tail"
  },
  "filter": {
    "filterCount": 2,
    "filterCondition": "head"
  }
}
```

### 示例4：关闭所有劫持

```json
{
  "enabled": false
}
```

## 使用方式

### 方式1：使用默认配置（最简单）

```typescript
import { installWithDefaultConfig } from 'vue-global-hijack';
await installWithDefaultConfig();
```

### 方式2：Vue 插件方式

```typescript
import VueGlobalHijack from 'vue-global-hijack';
app.use(VueGlobalHijack, { useDefault: true });
```

### 方式3：使用自定义配置地址

```typescript
import VueGlobalHijack from 'vue-global-hijack';
app.use(VueGlobalHijack, {
  configUrl: 'https://your-config-url/config.json'
});
```
