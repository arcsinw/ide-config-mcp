# IDE 配置文件 MCP 服务器

这是一个基于 Python编写的MCP Server，提供修改 IDE（目前只支持VS Code）配置文件的工具。MCP 允许大型语言模型（LLMs）直接调用这些工具来操作 IDE 设置。

## 功能特点

- 获取 IDE 配置文件内容
- 更新 IDE 配置文件
- 按 key 获取配置项
- 按 key 设置配置项
- 符合 MCP 标准，可被 LLMs 直接调用

## 安装指南

### 安装uv

参考https://uv.doczh.com/getting-started/installation/

### 配置ide-config-mcp

- Cursor

```json
{
  "mcpServers": {
    "ide-config-mcp": {
      "command": "uvx",
      "args": [
        "ide-config-mcp",
        "Cursor"
      ]
    }
  }
}
```

- VS Code

```json
{
  "mcpServers": {
    "ide-config-mcp": {
      "command": "uvx",
      "args": [
        "ide-config-mcp",
        "Code"
      ]
    }
  }
}
```

- Trae CN

```json
{
  "mcpServers": {
    "ide-config-mcp": {
      "command": "uvx",
      "args": [
        "ide-config-mcp",
        "TraeCN"
      ]
    }
  }
}
```

- Trae

```json
{
  "mcpServers": {
    "ide-config-mcp": {
      "command": "uvx",
      "args": [
        "ide-config-mcp",
        "Trae"
      ]
    }
  }
}
```

## 可用工具

### get_ide_settings
获取 VS Code 配置文件内容。

**返回**：配置文件的 JSON 内容

### update_ide_settings
更新 VS Code 配置文件。

**参数**：
- `settings`: 要更新的设置（字典格式）

**返回**：更新后的配置文件内容

### get_ide_setting_by_key
按 key 获取 VS Code 配置项。

**参数**：
- `key`: 配置项 key 名称

**返回**：包含配置值的字典，如果 key 不存在则返回错误信息。如果在用户设置中未找到key，会从默认设置中返回默认值。

### set_ide_setting_by_key
按 key 设置 VS Code 配置项。

**参数**：
- `key`: 配置项 key 名称
- `value`: 配置项的新值

**返回**：更新后的配置值，如果更新失败则返回错误信息

### get_default_settings
获取 VS Code 默认配置项。

**参数**：

**返回**：json格式的所有的默认配置，包含注释

## 注意事项

1. 服务器会根据操作系统自动访问对应的 VS Code 配置文件：
   - Windows: `%APPDATA%\Code\User\settings.json`
   - macOS: `~/Library/Application Support/Code/User/settings.json`
   - Linux: `~/.config/Code/User/settings.json`

2. 确保您的 LLM 支持 MCP 协议以自动发现和调用工具。