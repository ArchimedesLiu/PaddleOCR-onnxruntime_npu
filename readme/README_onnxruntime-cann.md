本仓库已在onnx逻辑中添加了npu使用逻辑，以PP-OCRv5运行示例可参考如下。

注意：昇腾设备建议使用镜像进行操作。此处提供910A的镜像获取方式（镜像需要权限，如需邮件联系:2671289934@qq.com）。
```
docker pull swr.cn-east-334.jnaicc.com/jnjacc/paddle-npu:cann80T113-ubuntu20-npu-910a-base-aarch64-gcc84
```

**文本识别：**
```python
python tools/infer/predict_det.py --image_dir="../ocr_test.png" --det_model_dir="../paddleocrv5/PP-OCRv5_server_det/inference.onnx" --use_npu=True --use_onnx=True
```
FAQ:如果遇到报错ImportError: /usr/local/lib/python3.10/dist-packages/simsimd./libgomp-947d5fa1.so.1.0.0: cannot allocate memory in static TLS block，请执行以下命令：
```
export LD_PRELOAD=/usr/local/lib/python3.10/dist-packages/simsimd./libgomp-947d5fa1.so.1.0.0
```

**文本检测：**
```python
python tools/infer/predict_rec.py --image_dir="../imagesno.jpg" --rec_model_dir="../paddleocrv5/PP-OCRv5_server_rec/inference.onnx" --use_npu=True --use_onnx=True --rec_char_dict_path="./ppocr/utils/dict/ppocrv5_dict.txt"
```