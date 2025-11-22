# Kyudo Simulation (弓道射法模擬)

這是一個基於 Web 的弓道（Kyudo）射法模擬器，旨在模擬弓道中的「射法八節」流程以及射擊體驗。

## ✨ 特色

*   **射法八節模擬**：完整呈現從足踏み (Ashibumi) 到 殘心 (Zanshin) 的八個階段動畫。
*   **視覺升級 (Visuals)**：
    *   **向量風格射手**：穿著標準弓道服（弓道衣、袴、足袋）與精細裝備（竹弓、弽）。
    *   **擬真道場場景**：包含安土、標靶聚光燈與道場牆面細節。
*   **物理模擬**：
    *   可調整弓力 (10-30 kg) 與 箭重 (20-35 g)
    *   **真實彈道計算**：基於能量守恆與重力下墜，動態計算拋物線。
    *   **模擬呼吸震幅**：可調整呼吸造成的瞄準晃動 (0-15)。
*   **視覺回饋**：
    *   **主視角**：模擬射手的第一人稱視角。
    *   **SVG 動畫窗格**：左側顯示射手骨架與動作細節，包含真實的握弓 (Tenouchi) 動態。
    *   **重播系統 (Replay)**：
        *   **靶面特寫**：當箭矢中靶或接近靶心時，顯示靶面落點。
        *   **鷹眼視角 (Hawk-Eye)**：以**射手視角**呈現 3D 立體拋物線軌跡，弧度由物理引擎動態計算。
*   **音效系統**：包含發射與中靶的音效回饋。

## 🎮 操作指南

1.  **啟動流程**：
    *   開啟網頁後，左側面板會顯示「射法八節」的進度。
    *   系統會自動進行動作演示，直到進入 **「会 (Kai)」** 階段。

2.  **瞄準與發射**：
    *   當進入「会」階段時，**[發射 (Hanare)]** 按鈕會亮起並閃爍。
    *   **瞄準**：
        *   使用 **方向鍵 (↑ ↓ ← →)** 微調準心位置。
        *   或使用 **滑鼠/觸控** 拖曳畫面進行瞄準。
    *   **發射**：
        *   按下 **空白鍵 (Space)** 或點擊 **[發射]** 按鈕。

3.  **參數調整**：
    *   左側面板可即時調整：
        *   **弓力 (10-30 kg)**：影響箭矢初速與射程
        *   **箭重 (20-35 g)**：影響彈道下墜幅度
        *   **左右瞄準修正 (Azuke)**：水平瞄準偏移量
        *   **上下瞄準修正 (Height)**：垂直瞄準偏移量
        *   **呼吸震幅 (Breath 0-15)**：模擬呼吸與手部晃動強度

4.  **結果判定**：
    *   **皆中 (Kaichū)!!** - 距離靶心 5cm 內（黃色）
    *   **中 (Atari)!** - 命中靶面 18cm 內（綠色）
    *   **殘念 (Zannen)** - 脫靶但在 5m 範圍內（灰色）
    *   **脫靶 (Out of Range)** - 完全脫離射程

5.  **重新開始**：
    *   射擊完成後，按 **空白鍵** 或 **Enter** 重新進入射法八節流程。

## 🎯 遊玩技巧

*   **瞄準要領**：
    *   靶心位於畫面中央偏右位置，約在準心水平線上。
    *   呼吸震幅越大，瞄準難度越高，建議初學者從低數值開始。
    *   長按方向鍵可以連續移動瞄準點，適合大範圍調整。

*   **物理參數建議**：
    *   **標準設定**：弓力 15kg、箭重 28g（接近實際弓道用具）
    *   **高弧度**：增加箭重或減少弓力，觀察拋物線彈道
    *   **遠射模式**：最大弓力 30kg、最輕箭重 20g

*   **重播系統觀察**：
    *   命中時會顯示 **靶面特寫**，可觀察落點位置。
    *   脫靶時會顯示 **鷹眼視角**，呈現側面彈道軌跡與落點。

## 🚀 快速開始

```bash
# 方法一：直接開啟 HTML 檔案
open index.html

# 方法二：使用本地伺服器（推薦）
python3 -m http.server 8000
# 然後在瀏覽器開啟 http://localhost:8000
```

## 📱 裝置支援

*   **桌面瀏覽器**：完整體驗，建議使用 Chrome、Firefox、Safari 或 Edge
*   **行動裝置**：支援觸控操作與響應式佈局
*   **音效**：需要使用者互動後才會啟動（瀏覽器安全政策）

## 🎨 技術特色

*   **純前端實作**：無需後端伺服器或建構工具
*   **SVG 向量動畫**：流暢的射手動作演示（全日本弓道連盟 ANKF 標準姿勢）
*   **真實物理引擎**：基於能量守恆與拋物線運動的彈道計算，並**即時驅動視覺軌跡**。
*   **Web Audio 音效**：程序化生成音效，無需外部音訊檔案

## 📝 射法八節 (Hassetsu)

1.  **足踏み (Ashibumi)** - 站立定位
2.  **胴造り (Dōzukuri)** - 調整身體姿勢
3.  **打起し (Uchiokoshi)** - 舉弓至 45 度
4.  **大三 (Daisan)** - 展開至「大」字形
5.  **引分け (Hikiwake)** - 拉弦擴張
6.  **会 (Kai)** - 滿引蓄力（可發射階段）
7.  **離れ (Hanare)** - 放箭
8.  **殘心 (Zanshin)** - 維持姿勢收尾

## 📄 授權

本專案為開源教育用途，歡迎學習與改進。

---

# Kyudo Simulation (English)

This is a web-based Kyudo (Japanese Archery) simulation designed to simulate the "Shaho Hassetsu" (Eight Stages of Shooting) and the shooting experience.

## ✨ Features

*   **Shaho Hassetsu Simulation**: Fully demonstrates the eight stages of shooting from Ashibumi to Zanshin.
*   **Visual Upgrades**:
    *   **Vector Style Archer**: Features traditional Kyudo attire (Gi, Hakama, Tabi) and detailed equipment (Bamboo Bow, Yugake).
    *   **Realistic Dojo Scene**: Includes Azuchi (sand bank), target spotlight, and detailed dojo walls.
*   **Physics Simulation**:
    *   Adjustable Bow Power (10-30 kg) and Arrow Weight (20-35 g).
    *   **Realistic Ballistics**: Dynamic parabolic trajectory calculation based on energy conservation and gravity.
    *   **Breath Simulation**: Adjustable aiming sway caused by breathing (0-15).
*   **Visual Feedback**:
    *   **Main View**: Simulates the archer's first-person perspective.
    *   **SVG Animation Pane**: Displays the archer's skeleton and motion details on the left, including realistic Tenouchi (grip) dynamics.
    *   **Replay System**:
        *   **Target Close-up**: Shows the impact point on the target face when the arrow hits or is close.
        *   **Hawk-Eye View**: Displays a 3D parabolic trajectory from the **shooter's perspective** when the arrow misses but is within range, with the arc dynamically driven by the physics engine.
*   **Audio System**: Includes sound feedback for shooting and hitting the target.

## 🎮 Operation Guide

1.  **Startup Process**:
    *   Upon opening the page, the left panel displays the progress of "Shaho Hassetsu".
    *   The system automatically demonstrates the movements until it enters the **"Kai"** stage.

2.  **Aiming and Shooting**:
    *   When entering the "Kai" stage, the **[Hanare]** button will light up and flash.
    *   **Aiming**:
        *   Use **Arrow Keys (↑ ↓ ← →)** to fine-tune the sight position.
        *   Or use **Mouse/Touch** to drag the screen for aiming.
    *   **Shooting**:
        *   Press **Spacebar** or click the **[Hanare]** button.

3.  **Parameter Adjustment**:
    *   Adjustable in real-time via the left panel:
        *   **Bow Power (10-30 kg)**: Affects initial velocity and range.
        *   **Arrow Weight (20-35 g)**: Affects trajectory drop.
        *   **Azuke (Horizontal Aim)**: Horizontal aiming offset.
        *   **Height (Vertical Aim)**: Vertical aiming offset.
        *   **Breath (0-15)**: Simulates the intensity of sway caused by breathing.

4.  **Result Judgment**:
    *   **Kaichū (All Hit)!!** - Within 5cm of the center (Yellow).
    *   **Atari (Hit)!** - Within 18cm of the target face (Green).
    *   **Zannen (Regret)** - Missed but within 5m range (Grey).
    *   **Out of Range** - Completely out of range.

5.  **Restart**:
    *   After shooting, press **Spacebar** or **Enter** to restart the Shaho Hassetsu process.

## 🎯 Gameplay Tips

*   **Aiming Essentials**:
    *   The target center is located slightly to the right of the screen center, approximately on the horizontal line of the sight.
    *   Higher breath amplitude makes aiming more difficult; beginners are advised to start with low values.
    *   Long-press arrow keys for continuous movement, suitable for large adjustments.

*   **Physics Parameter Suggestions**:
    *   **Standard Setting**: 15kg Bow, 28g Arrow (Close to actual Kyudo equipment).
    *   **High Arc**: Increase arrow weight or decrease bow power to observe the parabolic trajectory.
    *   **Long Range Mode**: Max bow power 30kg, lightest arrow 20g.

*   **Replay System Observation**:
    *   **Target Close-up** is shown on hit to observe the impact point.
    *   **Hawk-Eye View** is shown on miss to visualize the side trajectory and landing point.

## 🚀 Quick Start

```bash
# Method 1: Open HTML file directly
open index.html

# Method 2: Use local server (Recommended)
python3 -m http.server 8000
# Then open http://localhost:8000 in your browser
```

## 📱 Device Support

*   **Desktop Browser**: Full experience, Chrome, Firefox, Safari, or Edge recommended.
*   **Mobile Device**: Supports touch operation and responsive layout.
*   **Audio**: Requires user interaction to start (Browser security policy).

## 🎨 Technical Features

*   **Pure Frontend Implementation**: No backend server or build tools required.
*   **SVG Vector Animation**: Smooth archer motion demonstration (ANKF standard posture).
*   **Real Physics Engine**: Ballistics calculation based on energy conservation and parabolic motion, **driving visual trajectory in real-time**.
*   **Web Audio**: Procedurally generated sound effects, no external audio files needed.

## 📝 Shaho Hassetsu (Eight Stages)

1.  **Ashibumi** - Footing
2.  **Dōzukuri** - Correcting the Posture
3.  **Uchiokoshi** - Raising the Bow
4.  **Daisan** - Drawing the Bow (Third Stage)
5.  **Hikiwake** - Drawing Apart
6.  **Kai** - Full Draw (Ready to shoot)
7.  **Hanare** - Release
8.  **Zanshin** - Remaining Form / Continuation

## 📄 License

This project is for open-source educational purposes. Learning and improvement are welcome.

