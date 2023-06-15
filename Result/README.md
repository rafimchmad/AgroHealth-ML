# Model Result and Evaluation

From models created, we tested them to **test** folder and **Testing** folder. **test** folder contains test images from [New Plant Diseases Dataset](https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset) as the example images if the leaves are scanned on a flat plane, and **Testing** folder contains random images we found on Google to reflect scanning the image of the leaves directly on the plant.

From models testing, we get the following results:

## Self-Made Models
Self-Made models were made using convolutional neural networks from scratch, for example:
```Python
model = Sequential([
    Conv2D(32, (3,3), activation='relu', input_shape=(256, 256, 3)),
    MaxPooling2D(2,2),
    Conv2D(64, (3,3), activation='relu'),
    MaxPooling2D(3,3),
    Flatten(),
    Dense(256, activation='relu'),
    Dense(256, activation='relu'),
    Dropout(0.25),
    Dense(38, activation='softmax')
])
```
| Model Name  | Result from **test** | Result from **Testing** | Note |
| ----------- | -------------------- | ----------------------- | ---- |
| self_v2     | 30/33                | 77/190                  | trained on 21 classes and target size 150, 150  |
| self_38     | 28/33                | 76/190                  | trained on 38 classes and target size 150, 150  |
| self_38_v2  | 21/33                | -/190                   | trained on 38 classes and target size 256, 256  |
| self_38_v3  | 29/33                | 42/190                  | trained on 38 classes and target size 150, 150  |
| baru        | 31/33                | 40/190                  | trained on 38 classes, with additional augmentation and target size 256, 256  |
| baru1       | 27/33                | 52/190                  | trained on 38 classes, with additional augmentation and target size 256, 256  |
| baru2       | 30/33                | 45/190                  | trained on 38 classes, with additional augmentation and target size 256, 256  |
| baru3       | 24/33                | -/190                   | trained on 38 classes, with additional augmentation and target size 256, 256  |
| baru4       | 29/33                | 46/190                  | trained on 38 classes and target size 256, 256  |

## Transfer Learning
Transfer learning models were done by freezing the layers and adding several additional layers, like the following example:
```Python
model_mobilenetv2 = MobileNetV2(weights='imagenet',
                                include_top=False,
                                input_shape=(256, 256, 3))

for layer in model_mobilenetv2.layers:
    layer.trainable = False
```

```Python
model = tf.keras.Sequential([
    model_mobilenetv2,
    tf.keras.layers.GlobalAveragePooling2D(),
    tf.keras.layers.Dense(512, activation='relu'),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.Dense(38, activation='softmax')
])
```
| Model Name  | Result from **test** | Result from **Testing** | Note |
| ----------- | -------------------- | ----------------------- | ---- |
| inceptionv3       | 27/33          | 86/190                  | trained on 21 classes and target size 256, 256  |
| inceptionv3_38    | 28/33          | 81/190                  | trained on 38 classes and target size 256, 256  |
| mobilenetv2_v3    | 31/33          | 69/190                  | trained on 21 classes and target size 256, 256  |
| mobilenetv2_38    | 29/33          | 58/190                  | trained on 38 classes and target size 256, 256  |
| mobilenetv2_38_v2 | 29/33          | 65/190                  | trained on 38 classes and target size 150, 150  |

Notes: 
* Both Result columns mean the number of images correctly detected compared to the total images in the folder
* If the model trained on 38 classes and only correctly detected the disease, it counted as 1
* The "-" indicates that the model is poorly created that it didn't reach 25/33 (75% acc) on Result from **test**

## Conclusion
* Some of Self-Made models are prone to overfit, especially if `Dropout` layer wasn't used, for example as shown by model `baru` and `self_38_v3`. They are really good on **test** folder but get poor performance on **Testing** folder
* Adding augmentation was not required because the images in the dataset were already augmented
* The most stable models are achieved by `inceptionv3` and `inceptionv3_38`, as shown by table above. They are not as great as Self-Made models on **test** folder, but they got much better accuracy on **Testing** folder

