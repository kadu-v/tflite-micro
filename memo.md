# Memo

## Crotex-M3
- 32bit
[Cortex-M3のArmのサイト](https://www.arm.com/ja/products/silicon-ip-cpu/cortex-m/cortex-m3)

## ターゲットごとのビルドファイル
`/workspaces/tflite-micro/tensorflow/lite/micro/tools/make`

## x86_64用のStatic Libraryとバイナリの作成と実行
これを実行すると，`gen/linux_x86_64_default`にオブジェクトファイルと`libtensorflow-microlite.a`が作成される．
```bash
$ make -f tensorflow/lite/micro/tools/make/Makefile hello_world

# テストの実行
$ make -f tensorflow/lite/micro/tools/make/Makefile test

# バイナリの作成と実行
$ make -f tensorflow/lite/micro/tools/make/Makefile hello_world_bin
$ ./gen/linux_x86_64_default/bin/hello_world 
```
[プロジェクトのビルド方法](https://www.tensorflow.org/lite/microcontrollers/library?hl=ja)


## Static Libraryの生成
```bash
$ python3 tensorflow/lite/micro/tools/project_generation/create_tflm_tree.py \
    -e hello_world \
    -e micro_speech \
    -e person_detection \
    ./tmp/tflm-tree
$ cp ./tensorflow/lite/micro/tools/project_generation/Makefile ./tmp/tflm-tree/
$ cd ./tmp/tflm-tree
$ make -j8 examples
```


## arm926ej-sターゲットのStatic Libraryのビルド
```bash
$ python3 tensorflow/lite/micro/tools/project_generation/create_tflm_tree.py \
    -e hello_world \
    -e micro_speech \
    -e person_detection \
    ./tmp/tflm-tree
$ cp ./tensorflow/lite/micro/tools/project_generation/Makefile ./tmp/tflm-tree/
$ cd ./tmp/tflm-tree
$ make -j8 libtflm BUILD_TYPE=haneywell
```

