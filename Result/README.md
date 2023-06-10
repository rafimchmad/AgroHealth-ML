# Model Result and Evaluation

From models created, we tested them to **test** folder and **Testing** folder. **test** folder contains test images from [New Plant Diseases Dataset](https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset) as the example images if the leaves are scanned on a flat plane, and **Testing** folder contains random images we found on Google to reflect scanning the image of the leaves directly on the plant.

From models testing, we get the following results :
## Self-Made Models
| Model Name  | Result from **test** | Result from **Testing** | Note |
| ----------- | -------------------- | ----------------------- | ---- |
| self_v2     | 30/33                | 77/190                  | trained on 21 classes and images size 150, 150  |
| self_38     | 27/33                | 76/190                  | trained on 38 classes and images size 150, 150  |
| self_38_v2  |                      |                         | trained on 38 classes and images size 256, 256  |
| self_38_v3  | 28/33                |                         | trained on 38 classes and images size 150, 150  |
| baru        | 31/33                | 26/190                  | trained on 38 classes and images size 256, 256  |

## Transfer Learning
| Model Name  | Result from **test** | Result from **Testing** | Note |
| ----------- | -------------------- | ----------------------- | ---- |
| inceptionv3       | 27/33          |                   |   |
| inceptionv3_38    |           |                        |   |
| inceptionv3_38_v2 |           |                        |   |
| mobilenetv2_v3    |           |                        |   |
| mobilenetv2_38    |           |                        |   |
| mobilenetv2_38_v2 |           |                        |

Note: Both Result columns mean the number of images correctly detected compared to the total images in the folder
