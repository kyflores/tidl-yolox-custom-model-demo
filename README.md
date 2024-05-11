# TIDL YOLO-X custom model walkthrough
This repo is a fork of [WasabiFan's YOLOv5 compilation repo](https://github.com/WasabiFan/tidl-yolov5-custom-model-demo).
Instead of TI's YOLOv5 fork, it compiles a model from TI's [Megvii YOLO-X fork](https://github.com/TexasInstruments/edgeai-tensorlab/tree/main/edgeai-yolox).

For step by step instructions, please see [the original readme](./README_orig.md). Only the deviations are documented here.

The BeagleBone AI-64's 2023-10-07 image uses `v8.2` of the TIDL stack, so stick to these tags whenever there's an option.

# Why?
Megvii YOLO-X is apache 2.0 licensed, whereas YOLOv5 was GPL. Ultralytics include the model weights under the [AGPL license](https://www.ultralytics.com/license) of their newer models.

# Getting the model
To get TI's COCO pretrained model exported to onnx, download them using the [links in the modelzoo repo](https://github.com/TexasInstruments/edgeai-tensorlab/tree/r8.2/edgeai-modelzoo/models/vision/detection/coco/edgeai-yolox) You need both the `.onnx` and `.prototxt` files. I've tested with the `yolox-s-ti-lite_39p1_57p9` model, but I'd expect the smaller variants to work too. The `m` model had issues being compiled when I tried, perhaps it is too large for some limited resource.

To train your own model, you need to setup the [YOLO-X repo](https://github.com/TexasInstruments/edgeai-tensorlab/tree/main/edgeai-yolox) and follow the steps detailed there. To start from a pretrained model, use the `.checkpoint.pth` file in the modelzoo repo linked above, then follow the [export instructions](https://github.com/TexasInstruments/edgeai-tensorlab/blob/main/edgeai-yolox/README_2d_od.md#deployment).

NOTE: On 9May2024, many separate repos were consolidated in the `TexasInstruments/edgeai-tensorlab` repo. If you need the old YOLO-X, it's
[still up, but archived here](https://github.com/TexasInstruments/edgeai-yolox)

# Deviations
* Only the Python compile/inference scripts has been updated as of yet.
* The YOLO-X model takes images in [0-255] instead of [0-1].
    * I didn't check but I expect the scaling is just internal to the exported network.
