# shell-script
- **引用符**
  - シングルクォーテーション「'」の中はすべて文字列であると解釈される。
  - ダブルクォーテーション「"」の引用符内に変数があるとその内容が展開される。
- **文字列置換・削除**
  - ${変数%マッチパターン}
    - 後方からの検索の一致で一番初めにマッチした部分を削除
  - ${変数%%マッチパターン}
    - 後方からの検索の一致で一番後ろまでマッチした部分までを削除
  - ${変数#マッチパターン}
    - 前方からの検索の一致で一番初めにマッチした部分を削除
  - ${変数##マッチパターン}
    - 前方からの検索の一致で一番後ろまでマッチした部分までを削除
  - ${変数/文字列/処理後文字列}
    - 最初にマッチしたもののみ文字列を置換
  - ${変数//文字列/処理後文字列}
    - 全ての文字列を置換
  - ${変数名##*/}
    - ファイル名の取得
  - ${変数名%.*}
    - 拡張子の削除
  - ${変数名##*.}
    - 拡張子の取得
- **引数の指定**
  - ```
    #!/bin/sh

    echo Script name: $0

    echo Arguments: $1 $2 $3 $4 $5 $6 $7 $8 $9

    echo All arguments: $@

    exit 0
    ```
    実行結果
    ```
    $ sh script02.sh arg1 arg2 arg3 arg4 arg5 arg6 arg7 arg8 arg9
    Script name: script02.sh
    Arguments: arg1 arg2 arg3 arg4 arg5 arg6 arg7 arg8 arg9
    All arguments: arg1 arg2 arg3 arg4 arg5 arg6 arg7 arg8 arg9
    ```
  -  実行時の引数にファイルを渡すことも可能(ファイルの存在チェック)
- **条件分岐**
  - ```
    if [条件式1]; then
        処理1
    elif [条件式2]; then
        処理2
    fi
    ```
  - 実数の比較
    - `iflag=$(echo "scale=3;if( $var == 0.5 ) 1 else 0" | bc)`
    - パイプでbcを付ける  
- **変数**
  - `変数名=$(コマンド)`
    - コマンドの実行結果を引数として渡せる
  - =前後にスペースは空けない
- **繰り返し**
  - while文を使ったループ
    - ```
        #!/bin/sh

        i=1

        while [ $i -le 10 ]; do
            echo "i=$i"
            i=$(expr $i + 1)
        done

        exit 0
      ```
  -  for文を使ったループ
     -  ```
        #!/bin/sh

        wbc="sugiuchi utsumi yamaguchi sawamura yamai asao maeda imamura noumi"

        for player in $wbc; do
            echo $player
        done

        exit 0
        ```
- **配列の中身を全て参照**
  - スクリプト
    ```
    #!/bin/bash

    ARRAY=(0 1 2 3 4 5)

    echo "${ARRAY[@]}"
    ```
  - 実行結果 
    ```
    0 1 2 3 4 5 
    ```
- **case文**
  - bashにて特定の条件で処理を分岐させたい場合には、if文ではなくcase文を使用することもできます
  - ```
    STRINGS=(January February March April May June July August September October November December)
    for str in ${STRINGS[@]}
    do
        case $str in
            January )
                echo "$str は1月です"
            ;;
            February )
                echo "$str は2月です"
            ;;
            March )
                echo "$str は3月です"
            ;;
            * )
            echo "$str は1～３月ではありません"
        esac
    done
    ```