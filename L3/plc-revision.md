# PLC Ladder Logic — Revision Notes

> *PLC 梯形圖複習筆記* | Level 3 | MC-091-3:2016

---

## 1. PLC Scan Cycle / PLC 掃描循環

```
[Read Inputs] → [Execute Program (Top→Bottom, Left→Right)] → [Update Outputs] → Repeat
   讀取輸入          執行程序（上→下，左→右）                 更新輸出          重複
```

Every PLC runs this loop continuously. One pass = one **scan**. Typical scan time: 1-10 ms.

每台 PLC 都不斷跑這個循環。一圈 = 一個 **scan**。一般 scan time：1-10 ms。

---

## 2. Basic Symbols / 基本符號

| Symbol | Name | Function |
|---|---|---|
| `--[ ]--` | Normally Open (NO) Contact / 常開接點 | TRUE when input = ON |
| `--[\]--` | Normally Closed (NC) Contact / 常閉接點 | TRUE when input = OFF |
| `--( )--` | Output Coil / 輸出線圈 | Energize when rung is TRUE |
| `--(/)--` | Negated Output / 反相輸出 | Energize when rung is FALSE |

---

## 3. Logic Gates in Ladder / 邏輯閘轉梯形圖

### AND（串聯）
```
---[ ]-----[ ]-----( )---
   A       B       Y
```
Y = TRUE only when BOTH A AND B are ON. / A和B都ON時Y才ON。

### OR（並聯）
```
---[ ]--+-----( )---
   A    |
---[ ]--+
   B
```
Y = TRUE when A OR B is ON. / A或B任一ON時Y就ON。

### NOT（反相）
```
---[\]-----( )---
   A       Y
```
Y = TRUE when A is OFF. / A OFF時Y ON。

### NAND
```
---[ ]-----[ ]-----[/]---
   A       B        Y
```
Y = TRUE when NOT(A AND B). / A和B同時ON時Y為OFF。

### NOR
```
---[ ]--+-----[/]---
   A    |
---[ ]--+      Y
   B
```
Y = TRUE when NOT(A OR B). / A或B任一ON時Y為OFF。

---

## 4. Set/Reset (Latch) / 自保持電路

```
---[ ]--+-----( )---    ← SET：按A，Y ON
   A    |      Y
---[ ]--+      |
   Y    |      |
---[\]--+      ← RESET：按B，Y OFF
   B
```

| Action | Result |
|---|---|
| Press A (momentary) | Y turns ON and stays ON |
| Release A | Y keeps ON (自保持) |
| Press B | Y turns OFF |

**記憶口訣**：按A開，按B關，中間用Y的接點跨過A實現自保。

---

## 5. Timers / 計時器

### TON — Timer ON Delay（延時ON）

```
---[ ]----------[TON]-----( )---
   A         T1, 5000     Y
```
When A = ON for 5 seconds → Y = ON.
A持續ON 5秒後 → Y才ON。

| Condition | T1 Accumulated | Y |
|---|---|---|
| A OFF | 0 | OFF |
| A ON for 2s | 2000 | OFF |
| A ON for 5s+ | 5000 | ON |
| A goes OFF | Reset to 0 | OFF |

### TOF — Timer OFF Delay（延時OFF）

```
---[ ]----------[TOF]-----( )---
   A         T1, 3000     Y
```
A = ON → Y immediately ON. A goes OFF → Y stays ON for 3 more seconds.

A變ON → Y立刻ON。A變OFF後 → Y再撐3秒才OFF。

### TP — Timer Pulse（脈衝計時器）

A goes ON → Y = ON for exactly T ms, then OFF regardless of A state.

A一ON → Y立刻ON維持恰好T毫秒後自動OFF，不管A是否還ON。

---

## 6. Counters / 計數器

### CTU — Count Up（上數）

```
---[ ]----------[CTU]-----( )---
   Sensor      C1, 10      Y
```
Y = ON after Sensor pulses 10 times.
Sensor觸發10次後Y才ON。

### CTD — Count Down（下數）

Starts at preset, counts down to 0.
從預設值開始往下數到0。

---

## 7. Common Patterns / 常見模式

### Motor Start/Stop（馬達啟停）
```
---[START]--+----[STOP]-----(MOTOR)---
            |       \|
            +----[MOTOR]---
```
Standard 3-wire control. / 標準三線控制。

### Alternating Output（交替輸出 / 單鍵開關）
```
---[BTN]-----[CTU]-----
             C1, 2
---[C1.Q]-----( )---   ← C1 accumulated = 1 → Q ON
---[C1.Q]-----[CTD]--- ← Count down (auto reset at 2)
             C1, 2
```
One button: press once = ON, press again = OFF.

---

## 8. Quick Reference / 速查表

| Task / 任務 | Pattern / 模式 |
|---|---|
| Two conditions must both be true | Series contacts (AND) / 串聯接點 |
| Either condition triggers output | Parallel contacts (OR) / 並聯接點 |
| Output stays ON after trigger | Latch (self-holding) / 自保持 |
| Delay before output turns ON | TON / 延時ON計時器 |
| Output stays ON for fixed time | TP / 脈衝計時器 |
| Count events before action | CTU / 上數計數器 |
| Motor start/stop | 3-wire control / 三線控制 |

---

## Practice Tool / 練習工具

**[PLC Simulator Online](https://plcsimulator.online)** — Free browser-based Ladder Logic simulator.
Build rungs, simulate, share. No download needed. Used by 250,000+ students.
