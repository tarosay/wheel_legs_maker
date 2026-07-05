# wheel_legs_maker

ホイールレッグ（渦状弧曲線のスポークを持つホイール）を設計し、CADデータとして出力するブラウザツールです。
インストール不要・HTML1ファイルで動作します。

A browser-based design tool for "wheel legs" (wheels with spiral-arc spokes). It exports DXF (for 2D CAD such as JW-CAD) and point curve text files (for DesignSpark Mechanical).

## 使い方

次のURLをブラウザで開くだけです。

```
https://tarosay.github.io/wheel_legs_maker/
```

ローカルで使う場合は [docs/index.html](docs/index.html) を直接開いても動作します。

### 調整できるパラメータ

| パラメータ | 説明 |
|---|---|
| 外径 D | ホイールの外径 [mm] |
| レッグ幅 | スポーク（レッグ）の幅 [mm] |
| レッグ本数 N | 360°/N 間隔で等分配置 |
| 巻き角度 sweep | 渦の巻き込み角度 [deg]（負値で逆巻き） |
| 半径増加指数 | 半径の増え方（1=線形、<1=外側で緩く、>1=外側で急に） |
| 開始半径 r0 | レッグの開始位置（ハブ半径） [mm] |
| 分割数 | 曲線の折れ線近似の点数 |

- 各パラメータは数値入力とスライダーの両方で操作できます。
- キャンバス上で終点 P1 をドラッグすると、外径円上で終点角度を変えられます。
- 「巻き方向を反転」ボタンで渦の向きを反転します。

## 出力形式

### DXF（JW-CAD などの2D CAD向け）

- DXF R12（AC1009）形式。JW-CAD で読み込めることを確認しています。
- レイヤ構成: `OUTER_DIAMETER`（外径円）/ `CENTER_LINE`（レッグ中心線）/ `LEG_OUTLINE`（レッグ外形線）
- すべて実線・黒（色番号7）で出力します。
- 寸法は入力した mm 値そのままです（画面表示のみ自動縮尺）。

### point curve .txt（DesignSpark Mechanical 向け）

レッグ外形線（閉じたスプライン）のみを、DesignSpark Mechanical の点列カーブ形式で出力します。

DesignSpark Mechanical でソリッド化する手順:

1. 「挿入 → ファイル」で .txt を読み込む（閉じたスプラインカーブになります）
2. カーブを選択して「塗りつぶし」（面が張られます）
3. 面を「プル」で押し出してソリッド化

> メモ: 点列を折れ線（`polyline=true`）で読み込むと「塗りつぶし」が失敗するため、スプラインで出力しています。

## ライセンス

[MIT License](LICENSE)
