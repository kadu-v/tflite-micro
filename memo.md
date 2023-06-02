# Static Libraryの生成
```bash
$ python3 tensorflow/lite/micro/tools/project_generation/create_tflm_tree.py \
    -e hello_world \
    -e micro_speech \
    -e person_detection \
    ./tmp/tflm-tree
$ cp ./tflite-micro/tensorflow/lite/micro/tools/project_generation/Makefile ./tmp/tflm-tree/
$ cd ./tmp/tflm-tree
$ make -j8 examples
```