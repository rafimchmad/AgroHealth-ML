# Model Result and Evaluation

From models created, we tested them to **test** folder and **Testing** folder. **test** folder contains test images from [New Plant Diseases Dataset](https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset) as the example images if the leaves are scanned on a flat plane, and **Testing** folder contains random images we found on Google to reflect scanning the image of the plant directly on the plant.

From models testing, we get the following results :
## Self-Made Models
| Model Name  | Result from **test** | Result from **Testing** | Note |
| ----------- | -------------------- | ----------------------- | ---- |
| self_v2     | 30/33                | 77/190                  |      |
| self_38     | 28/33                | 76/190                  |      |
| self_38_v2  |                      |                         |      |
| self_38_v3  | 28/33                |                         |      |
| baru        | 31/33                | 26/190                  |      |

## Transfer Learning


Note: Both Result columns mean the number of images correctly detected compared to the total images in the folder
