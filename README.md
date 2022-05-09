# peoplesegnet-on-tao-toolkit
peoplesegnet-on-tao-toolkit は、NVIDIA TAO TOOLKIT を用いて PeopleSegNet の AIモデル最適化を行うマイクロサービスです。  

## 動作環境
- NVIDIA 
    - TAO TOOLKIT
- PeopleSegNet
- Docker
- TensorRT Runtime

## PeopleSegNetについて
PeopleSegNet は、画像内の人を検出し、セグメント化されたインスタンスとカテゴリラベルを返すAIモデルです。  
PeopleSegNet は、特徴抽出にResNet50を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順

### engineファイルの生成
PeopleSegNet のAIモデルをデバイスに最適化するため、ResNet50 における PeopleSegNet の .etlt ファイルを engine file に変換します。
engine fileへの変換は、Makefile に記載された以下のコマンドにより実行できます。

```
tao-convert:
	docker exec -it peoplesegnet-tao-toolkit tao-converter -k nvidia_tlt -t fp16 -d 3,576,960 -e /app/src/peoplesegnet_resnet50.etlt_b1_gpu0_fp16.engine /app/src/peoplesegnet_resnet50.etlt

```

## 相互依存関係にあるマイクロサービス  
本マイクロサービスで最適化された PeopleSegNet の AIモデルを Deep Stream 上で動作させる手順は、[peoplesegnet-on-deepstream](https://github.com/latonaio/peoplesegnet-on-deepstream)を参照してください。  

## engineファイルについて
engineファイルである peoplesegnet.engine は、[peoplesegnet-on-deepstream](https://github.com/latonaio/peoplesegnet-on-deepstream)と共通のファイルであり、本レポジトリで作成した engineファイルを、当該リポジトリで使用しています。  
