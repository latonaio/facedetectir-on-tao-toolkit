# facedetectir-on-tao-toolkit
facedetectir-on-tao-toolkit は、NVIDIA TAO TOOLKIT を用いて FaceDetectIR の AIモデル最適化を行うマイクロサービスです。  

## 動作環境
- NVIDIA 
    - TAO TOOLKIT
- FaceDetectIR
- Docker
- TensorRT Runtime

## FaceDetectIRについて
FaceDetectIR は、画像内の顔を検出し、カテゴリラベルを返すAIモデルです。  
FaceDetectIR は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順

### engineファイルの生成
FaceDetectIR のAIモデルをデバイスに最適化するため、ResNet18 における FaceDetectIR の .etlt ファイルを engine file に変換します。
engine fileへの変換は、Makefile に記載された以下のコマンドにより実行できます。

```
tao-convert:
	docker exec -it facedetectir-tao-toolkit tao-converter -k tlt_encode -t fp16 -d 3,240,384 -e /app/src/facedetectir.engine /app/src/resnet18_facedetectir_pruned.etlt
```

## 相互依存関係にあるマイクロサービス  
本マイクロサービスで最適化された FaceDetectIR の AIモデルを Deep Stream 上で動作させる手順は、[facedetectir-on-deepstream](https://github.com/latonaio/facedetectir-on-deepstream)を参照してください。  

## engineファイルについて
engineファイルである facedetectir.engine は、[facedetectir-on-deepstream](https://github.com/latonaio/facedetectir-on-deepstream)と共通のファイルであり、本レポジトリで作成した engineファイルを、当該リポジトリで使用しています。  
