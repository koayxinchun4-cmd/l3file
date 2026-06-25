# AutoCAD — Mechanical Drawing Revision Notes

> *AutoCAD 機械繪圖複習筆記* | Level 3 | MC-091-3:2016

---

## 1. Setup First / 開檔第一件事

```
UNITS   → Type: Decimal, Precision: 0.00, Insertion scale: Millimeters
LIMITS  → A3: 420,297  |  A4: 297,210
ZOOM    → A (to fit limits on screen)
LAYER   → Create: Visible, Hidden, Centre, Dimension, Text
```

Save as `.dwt` template. Do this ONCE, reuse forever.

存成 `.dwt` 範本，設一次用一輩子。

---

## 2. Coordinate System / 坐標系統

| Mode | Syntax | Example | Meaning |
|---|---|---|---|
| **Absolute** | `X,Y` | `50,75` | From origin (0,0) / 從原點算 |
| **Relative** | `@X,Y` | `@100,0` | From last point, 100mm right / 從上一點往右100mm |
| **Polar Relative** | `@dist<angle` | `@50<45` | 50mm at 45° / 距離50，角度45° |

```
      Y ↑
        |
   (50,75)
        |
(0,0)──*────→ X
```

---

## 3. Essential Drawing Commands / 核心繪圖指令

### Lines & Shapes / 線條與形狀

| Command | Shortcut | What It Does |
|---|---|---|
| LINE | `L` | Draw line segments / 畫線段 |
| CIRCLE | `C` | Circle by center+radius or 2P/3P / 圓 |
| RECTANGLE | `REC` | Rectangle by 2 corners / 矩形 |
| ARC | `A` | Arc by 3 points or center+start+end / 弧 |
| POLYGON | `POL` | Regular polygon (3-1024 sides) / 正多邊形 |
| ELLIPSE | `EL` | Ellipse by axis endpoints / 橢圓 |
| POLYLINE | `PL` | Connected line+arc segments as one object / 聚合線 |

### Modify / 修改

| Command | Shortcut | What It Does |
|---|---|---|
| ERASE | `E` | Delete selected objects / 刪除 |
| TRIM | `TR` | Cut lines at intersection / 修剪到邊界 |
| EXTEND | `EX` | Extend line to boundary / 延伸到邊界 |
| OFFSET | `O` | Create parallel copy at distance / 偏移複製 |
| MIRROR | `MI` | Mirror objects across axis / 鏡像 |
| ARRAY | `AR` | Rectangular or polar pattern / 陣列 |
| FILLET | `F` | Round corner with radius / 倒圓角 |
| CHAMFER | `CHA` | Bevel corner with distances / 倒角 |
| SCALE | `SC` | Resize objects / 縮放 |
| ROTATE | `RO` | Rotate objects / 旋轉 |
| MOVE | `M` | Move objects / 移動 |
| COPY | `CO` | Duplicate objects / 複製 |
| EXPLODE | `X` | Break block/polyline into parts / 分解 |

---

## 4. Object Snaps (OSNAP) / 物件鎖點

Press `F3` to toggle. Critical for precision. / 按F3開關，精準繪圖的命脈。

| Snap | Key | Snaps To |
|---|---|---|
| ENDpoint | END | End of line/arc / 端點 |
| MIDpoint | MID | Middle of line/arc / 中點 |
| CENter | CEN | Center of circle/arc / 圓心 |
| QUAdrant | QUA | 0°/90°/180°/270° of circle / 象限點 |
| INTersection | INT | Where lines cross / 交點 |
| PERpendicular | PER | 90° to line / 垂直點 |
| TANgent | TAN | Tangent to circle/arc / 切點 |

---

## 5. Orthographic Projection / 正交投影

Standard 3-view drawing: / 標準三視圖：

```
      ┌─────────┐
      │   TOP   │
      │  上視圖  │
┌─────┼─────────┼─────┐
│LEFT │ FRONT   │RIGHT│
│左視 │ 前視圖   │右視 │
└─────┴─────────┴─────┘
```

| View | Position | Shows |
|---|---|---|
| Front（前視） | Center | Height + Width |
| Top（上視） | Above front | Width + Depth |
| Right side（右側視） | Right of front | Height + Depth |

**Rule**: Top aligns vertically with Front. Side aligns horizontally with Front.

**規則**：上視圖和前視圖垂直對齊。側視圖和前視圖水平對齊。

---

## 6. Dimensioning / 尺寸標註

| Type | Command | Use |
|---|---|---|
| Linear | `DIMLIN` / `DLI` | Horizontal or vertical / 水平或垂直 |
| Aligned | `DIMALI` / `DAL` | Parallel to angled line / 與斜線平行 |
| Radius | `DIMRAD` / `DRA` | Circle/arc radius / 半徑 |
| Diameter | `DIMDIA` / `DDI` | Circle diameter / 直徑 |
| Angular | `DIMANG` / `DAN` | Angle between lines / 角度 |
| Baseline | `DIMBASE` / `DBA` | Stack from common baseline / 從基準堆疊 |
| Continue | `DIMCONT` / `DCO` | Chain from previous / 連續標註 |

---

## 7. Layers & Line Types / 圖層與線型

| Layer Name | Color | Line Type | Lineweight | Use |
|---|---|---|---|---|
| Visible | White/Black | Continuous | 0.50 mm | Object outlines / 物體輪廓 |
| Hidden | Yellow | HIDDEN2 | 0.30 mm | Hidden edges / 隱藏邊 |
| Centre | Red | CENTER2 | 0.20 mm | Center lines / 中心線 |
| Dimension | Cyan | Continuous | 0.20 mm | Dimensions / 標註 |
| Text | Green | Continuous | 0.20 mm | Notes and labels / 文字 |
| Title Block | Magenta | Continuous | 0.30 mm | Drawing border / 圖框 |

---

## 8. Quick Reference / 速查表

| Task | Commands |
|---|---|
| Start new mechanical drawing | `UNITS` → `LIMITS` → `ZOOM A` → make layers |
| Draw a rectangle 100x50mm at (10,10) | `REC` → `10,10` → `@100,50` |
| Fillet corner R=5mm | `F` → `R` → `5` → pick 2 lines |
| Create parallel line 20mm away | `O` → `20` → pick line → pick side |
| Add center line to a circle | Switch to Centre layer → `L` → snap to QUA or CEN |
| Copy object 3 times, 30mm apart | `AR` (rectangular) → rows=1, cols=4, spacing=30 |
| Dimension a horizontal line | `DLI` → pick 2 endpoints → place text |

---

## Free Alternative / 免費替代軟體

**[DraftSight](https://www.draftsight.com)** — Interface nearly identical to AutoCAD. Free for students.

介面幾乎跟 AutoCAD 一模一樣，學生免費。
