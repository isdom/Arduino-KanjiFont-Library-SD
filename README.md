# Arduino用漢字フォントライブラリ SDカード版
(本文書は現在作成中です)

## 概要
このライブラリはArduino用の漢字フォントドライバーライブラリです。  
SDカードに格納したフォントデータを逐次参照し、UTF-8コードに対応する漢字フォントデータの取得を可能にします。 

## ライブラリ名称
**sdfonts** (ヘッダーファイル sdfonts.h)

## 特徴
- フォントのサイズとして8,10,12,14,16,20,24の7種類をサポートします。
- UTF-8形式の文字の利用が可能です。
- フォントデータはSDカード(SPI接続)に格納しています。
- フォントデータの格納形式として２つの形式を提供します。  
  - 横並び形式(デフォルト)  
    <img src="img/type1.PNG" width="200">  
  - 縦並び形式（モノクログラフィック液晶用)  
    <img src="img/type2.PNG" width="200">  
  ※ 赤い数値はバイトデータの並び順  

## 利用環境
- Arduino Unoまたはその互換機
- 開発環境 Arduino IDE 1.6.5以降
- SPI接続、SDライブラリによるSDカードの利用ができること

## ハードウェア構成例
(後で図を入れて書く)  

## サポートするフォントの詳細
半角および、全角日本語ひらがな、カタカタ、漢字、英語アルファベット、ギリシャ文字,記号
半角カタカナはサポートしていません。半角カタカナのコードを指定した場合、全角カタカナに置き換えます。  

|フォントサイズ| 利用フォント    |フォント登録数|
|-------------:|-----------------|-------------:|
|8x4           |美咲半角フォント |191           |
|8x8           |美咲フォント     |6879          |
|10x5          |ナガ10 半角      |256           |
|10x10         |ナガ10           |6877          |
|12x6          |東雲半角フォント |256           |
|12x12         |東雲フォント     |6879          |
|14x7          |東雲半角フォント |256           |
|14x14         |東雲フォント     |6879          |
|16x8          |東雲半角フォント |256           |
|16x16         |東雲フォント     |6879          |
|20x10         |Kappa20 半角     |190           |
|20x20         |Kappa20          |6879          |
|24x12         |X11R6半角フォント|221           |
|24x24         |X11R6フォント    |6877          |

## インストール
* /liblary/sdfonts フォルダをArduinoのliblaryにコピーする。  
* /fontbin フォルダ内の FONT.BIN、FONTLCD.BIN  SDカードの直下に入れる。

## ライブラリリファレンス
ライブラリはオブジェクトとして実装しています。 
グローバルオブジェクト **SDfonts**のメンバー関数を呼び出すことにより、  
機能利用することが出来ます。  

**ヘッダファイル**  
   `#include <sdfonts.h>`

**定数一覧**  

    #define EXFONTNUM  14    // 登録フォント数
    #define FULL_OFST   7    // フォントサイズから全角フォント種類変換用オフセット値
    #define MAXFONTLEN  72   // 最大フォントバイトサイズ(=24x24フォント)
    #define MAXSIZETYPE 7    // フォントサイズの種類数
    // フォントサイズ
    #define  EXFONT8    0    // 8ドット美咲フォント
    #define  EXFONT10   1    // 10ドット nagaフォント
    #define  EXFONT12   2    // 12ドット東雲フォント
    #define  EXFONT14   3    // 14ドット東雲フォント
    #define  EXFONT16   4    // 16ドット東雲フォント
    #define  EXFONT20   5    // 20ドットkappa20フォント
    #define  EXFONT24   6    // 24ドットXフォント


**グローバルオブジェクト**  
`extern sdfonts SDfonts;`

**関数一覧**  
- 初期化  
  `bool init(uint8_t cs)`  
  フォント利用のための初期設定を行います。  
  
- グラフィック液晶モードの設定    
  `void setLCDMode(bool flg)`

- フォントファイルのオープン  
  `bool open(void)`

- フォントファイルのクローズ  
  `void close(void)`

- 利用サイズを番号で設定  
  `void setFontSizeAsIndex(uint8_t sz)`

- 現在利用フォントサイズ番号の取得  
  `uint8_t getFontSizeIndex()`

- 利用サイズ(ドット数)の設定  
  `void setFontSize(uint8_t sz)`

- 現在利用フォントサイズ(ドット数)の取得  
  `uint8_t getFontSize()`

- 指定したUTF16コードに該当するフォントデータの取得  
  `boolean getFontData(byte* fontdata,uint16_t utf16)`
  
- 指定したUTF8文字列の先頭のフォントデータの取得  
  `char* getFontData(byte* fontdata,char *pUTF8)`

- 横のバイト数取得  
  `uint8_t getRowLength()`

- 現在利用フォントの幅(ドット数)の取得  
  `uint8_t getWidth()`

- 現在利用フォントの高さ(ドット数)の取得  
  `uint8_t getHeight()`

- 現在利用フォントのデータサイズ(バイト)の取得  
  `uint8_t getLength()`

- 直前に処理した文字コード(utf16)の取得  
  `uint16_t getCode()`


## サンプルソースの解説

## ライセンス・使用条件
フォントライブラリのプログラム部に関しては製作者本人に帰属しますが、自由に利用下さい。
フォントデータに関しては、著作権はフォントの各製作者に帰属します。

 ・ 8ドットフォント  
    美咲フォント [フリー（自由な）ソフトウエア]  
    http://www.geocities.jp/littlimi/misaki.htm  
    ライセンスに関する記載 http://www.geocities.jp/littlimi/font.htm#license  

 ・ 10ドットフォント  
    ナガ10(1.1):[独自ライセンス]  
    http://hp.vector.co.jp/authors/VA013391/fonts/#naga10  
    ライセンスに関する記載 \knj10-1.1\README  

 ・12/14/16ドットフォント  
    東雲フォント(0.9.6):[public domain]  
    http://openlab.ring.gr.jp/efont/shinonome/index.html.ja  
    ライセンスに関する記載 同HP  

 ・20ドットフォント  
    Kappa 20dot fonts(0.3):[public domain]  
   http://kappa.allnet.ne.jp/20dot.fonts/(リンク切れ)  

 ・24ドットフォント  
  X11R6同梱のフォント:[(通称)X11ライセンス]  
   http://www.x.org  

本ライブラリおよび配布するファイルは上記フォントの二次加工ファイルを含むのため、  
ライセンスについはては  使用フォントのライセンスに従うものとします。  

使用しているナガ10について商用利用に関する制約記載があるため  
本配布ファイルも個人および非営利目的での利用のみとします。   

またナガ10フォントの配布条件に従い、オリジナルのフォントとドキュメントを添付します。  

再配布については、本構成のままであれば自由とします。  
フォントファイルのみの配布は禁止します。  





