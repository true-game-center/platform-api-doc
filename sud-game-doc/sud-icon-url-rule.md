# SUD 游戏图标 URL 规则

## 问题描述

SUD 厂商的游戏图标 URL 与其他厂商（heibao 系列、BG、apple-game 等）不同。
如果错误地使用了通用规则，会导致 SUD 游戏图标无法正常显示。

## 正确的 URL 格式

```
https://static.super86.cc/public-assets/images/game-asset/sud-game/{游戏ID}/square.webp
```

### 关键差异

| 项目 | SUD 游戏 | 其他厂商（heibao 等） |
|------|----------|----------------------|
| 域名 | `static.super86.cc` | `static.vietbet86.com` |
| 路径 | `sud-game` | `platform-game` |
| 资源 ID | 使用**游戏ID**（game-list 中第3列） | 使用平台分配的资源 ID |

### 示例

| 游戏名称 | 游戏ID | 正确图标 URL |
|----------|--------|-------------|
| BubbleShooter | 1465755837908648523 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1465755837908648523/square.webp` |
| EightBall | 1466136700248916605 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1466136700248916605/square.webp` |

### 错误示例

```
https://static.vietbet86.com/public-assets/images/game-asset/platform-game/1819318615915831298/square.webp
```

错误点：
1. 域名用了 `static.vietbet86.com`（应为 `static.super86.cc`）
2. 路径用了 `platform-game`（应为 `sud-game`）
3. 资源 ID 不是游戏 ID（应使用 game-list 中的游戏ID）

## 适用范围

- 厂商名称：**SUD**
- 厂商ID：`1465720586452861022`
- 当前游戏列表中共 11 款 SUD 游戏

## 修复方法

在 `game-list.md` 中，将 SUD 行的图标列按以下规则替换：

```
域名:       static.vietbet86.com  →  static.super86.cc
路径段:     platform-game         →  sud-game
资源ID:     替换为该行的「游戏ID」列值
```
