# vehiclemakenet-on-tao-toolkit
vehiclemakenet-on-tao-toolkit は、NVIDIA TAO TOOLKIT を用いて VehicleMakeNet の AIモデル最適化を行うマイクロサービスです。  

## 動作環境
- NVIDIA 
    - TAO TOOLKIT
- VehicleMakeNet
- Docker
- TensorRT Runtime

## VehicleMakeNetについて
VehicleMakeNet は、画像内の車を検出し、２０種類の車種に分類したカテゴリラベルを返すAIモデルです。  
VehicleMakeNet は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順

### engineファイルの生成
VehicleMakeNet のAIモデルをデバイスに最適化するため、ResNet18 における VehicleMakeNet の .etlt ファイルを engine file に変換します。
engine fileへの変換は、Makefile に記載された以下のコマンドにより実行できます。

```
tao-convert:
        docker exec -it vehiclemakenet-tao-toolkit tao-converter -k tlt_encode -t fp16 -d 3,224,224 -e /app/src/vehiclemakenet.engine /app/src/resnet18_vehiclemakenet_pruned.etlt
```

## 相互依存関係にあるマイクロサービス  
本マイクロサービスで最適化された VehicleMakeNet の AIモデルを Deep Stream 上で動作させる手順は、[vehiclemakenet-on-deepstream](https://github.com/latonaio/vehiclemakenet-on-deepstream)を参照してください。  

## engineファイルについて
engineファイルである vehiclemakenet.engine は、[vehiclemakenet-on-deepstream](https://github.com/latonaio/vehiclemakenet-on-deepstream)と共通のファイルであり、本レポジトリで作成した engineファイルを、当該リポジトリで使用しています。  
