# SUD 游戏图标 URL 规则

## 问题描述

SUD 厂商的游戏图标 URL 与其他厂商（heibao 系列、BG、apple-game 等）不同。
如果错误地使用了通用规则，会导致 SUD 游戏图标无法正常显示。

## 正确的 URL 格式

```
https://static.super86.cc/public-assets/images/game-asset/sud-game/{game_code}/square.webp
```

> **注意：URL 中使用的是 `game_code`（数据库 `game_info.game_code` 字段），不是 `id`（游戏ID）。**

### 关键差异

| 项目 | SUD 游戏 | 其他厂商（heibao 等） |
|------|----------|----------------------|
| 域名 | `static.super86.cc` | `static.vietbet86.com` |
| 路径 | `sud-game` | `platform-game` |
| 资源 ID | `game_code`（数据库 game_info 表） | 平台分配的资源 ID |

### game_code 获取方式

从数据库 `game-center.game_info` 表查询：

```sql
SELECT gi.id, gi.game_code, gi.third_game_id
FROM game_info gi
INNER JOIN game_supplier gs ON gi.supplier_id = gs.id
WHERE gs.game_supplier_code LIKE '%SUD%'
ORDER BY gi.id;
```

### 当前 SUD 游戏 gameId → game_code 映射

| 游戏名称 | 游戏ID (id) | game_code | 图标 URL |
|----------|-------------|-----------|----------|
| 友尽闯关 | 1465754605622133299 | 1490944230389182466 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1490944230389182466/square.webp` |
| teenpattipro | 1465755096695439931 | 1557194487352053761 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1557194487352053761/square.webp` |
| Domino | 1465755473591403075 | 1537330258004504578 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1537330258004504578/square.webp` |
| BubbleShooter | 1465755837908648523 | 1819318615915831298 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1819318615915831298/square.webp` |
| Bingo | 1465756116234273363 | 1964541611859566593 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1964541611859566593/square.webp` |
| Ludo | 1465756441661932123 | 1468180338417074177 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1468180338417074177/square.webp` |
| Lucky77Pro | 1465756975512945251 | 1900378861741793281 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1900378861741793281/square.webp` |
| Kungfu King | 1466135015652852340 | 1572529974711259138 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1572529974711259138/square.webp` |
| Soul Booster | 1466135397846221431 | 1890346721291059202 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1890346721291059202/square.webp` |
| Number Bomb | 1466135818807542394 | 1468091457989509190 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1468091457989509190/square.webp` |
| EightBall | 1466136700248916605 | 1739914495960793090 | `https://static.super86.cc/public-assets/images/game-asset/sud-game/1739914495960793090/square.webp` |

## 错误示例

```
# 错误1：使用了错误的域名和路径
https://static.vietbet86.com/public-assets/images/game-asset/platform-game/1819318615915831298/square.webp

# 错误2：使用了 gameId 而非 game_code
https://static.super86.cc/public-assets/images/game-asset/sud-game/1465755837908648523/square.webp
```

## 修复方法

1. 从数据库查询 SUD 游戏的 `game_code`
2. 在 `game-list.md` 中，将 SUD 行的图标列按以下规则替换：

```
域名:       static.vietbet86.com  →  static.super86.cc
路径段:     platform-game         →  sud-game
资源ID:     替换为该游戏的 game_code（从 game_info 表获取）
```

## 适用范围

- 厂商名称：**SUD**
- 厂商ID：`1465720586452861022`
- 数据库：`game-center`，表：`game_info` + `game_supplier`
