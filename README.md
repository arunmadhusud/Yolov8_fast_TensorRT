# Yolov8_fast_TensorRT

This project aims to increase the inference speed of the Yolov8 model. The Pytorch model is downloaded from the Ultralytics library. The model is converted to ONNX format and then to a TensorRT engine using the TensorRT Python API. The inference speed is compared between the Pytorch model, ONNX model, and TensorRT engine. The code is run on Google Colab. Only the base Pytorch model is downloaded from the Ultralytics library. Post-processing steps, including Non-Maximum Suppression (NMS), bounding box generation, and label creation, are implemented from scratch. This ensures that the model can be used with the TensorRT engine and ONNX model without relying on the Ultralytics library.

## Results

The average processing time for each frame is lower for the TensorRT engine compared to the Pytorch model and ONNX model. The output videos for the Pytorch model and TensorRT engine can be found at the following links:

- [Watch TensorRT results here](https://drive.google.com/file/d/130vOZHwt3mteeo0hgahW2v_IXt973yXZ/view?usp=drive_link)
- [Watch Pytorch results here](https://drive.google.com/file/d/1hFDYpUp72P7sF3UP--w2KJBMShrBYL-N/view?usp=drive_link)

The ONNX model was very slow, and hence the output video is not provided. The reason for slower inference in ONNX could be that the model is run using the `CPUExecutor`. I tried to run the model using `CUDAExecutor`. Even though the model was loaded on GPU, the inference session was still running with `CPUExecutor`. I believe this is due to the mismatch between the versions of `onnxruntime-gpu` (1.18), CUDA (12.2), and cuDNN (8.9.6). The required versions are `onnxruntime-gpu` (1.18), CUDA (12.4), and cuDNN (8.9.2.26) as mentioned in the [ONNX Runtime documentation](https://onnxruntime.ai/docs/execution-providers/CUDA-ExecutionProvider.html#requirements).


