# NYBG IMAGE CLASSIFIER🌱
## Project Overview
For the Break Through Tech AI Spring project, we partnered with The New York Botanical Garden. The New York Botanical Garden(NYBG) herbarium houses over 7.8 million plant and fungal specimens, offering invaluable insights into plant diversity and ecological changes over time. However, approximately 10% of the digitized images in the database are classified as “non-standard,” including images of animals and color illustrations, which hinder researchers' ability to conduct meaningful machine learning studies.

This project aims to develop a machine learning model that automatically classifies and filters out non-standard images, facilitating more efficient dataset curation for biodiversity research.
![00a0b08c8e84c1c8](https://github.com/user-attachments/assets/d8fe5c29-d6de-4e59-aab8-54f01c1f234a)
![0a1d293939393939](https://github.com/user-attachments/assets/4311a1ac-3358-46e4-81b0-8e55266ddb15)
![0a0a49cfc7474f4f](https://github.com/user-attachments/assets/ad18f0ce-3e0c-41c8-bee8-eecda8c30bc8)

## Project Scope
- <b>Objective:</b> To create a robust image classification model capable of distinguishing between standard and non-standard herbarium images.
- <b>Target Audience:</b> Researchers and scientists utilizing NYBG’s herbarium data for ecological studies, biodiversity analysis, and conservation efforts.
- <b>Impact:</b> Streamline the data curation process, enabling researchers to focus on significant biodiversity research while enhancing the usability of the dataset.

For this project, we classified 122,880 samples of specimens into the 10 image classes.

## 10 Image classes
1. Occuluded Specimens
2. Microscope Slides
3. Illustrations (Color)
4. Animal Specimens
5. Live Plants
6. Biocultural Specimens: Human made objects; brooms, carpets, etc.
7. Illustrations (Gray)
8. Mixed Pressed Specimens
9. Ordinary Pressed Specimens
10. Micrographs Transmission Light

Our most accurate model lies in the 'epoch.ipynb' file. Through a Tensorflow Xception Model, we achieved an accuracy score over 90%. This competition was sourced through kaggle and you can find our team's submission here: https://www.kaggle.com/competitions/bttai-nybg-2024/overview

## **Our Objectives:**
- [ ] Exploratory Data Analysis
- [ ] Model Creation
- [ ] Hyperparameter Tuning
- [ ] Performance

> [!NOTE]
> Our data was previously seperated into 3 datasets.
> Training data with 81,946 rows and 5 columns.
> Validation data with 10,244 rows and 5 columns.
> Test data with 30,690 rows and 2 columns.


## **EDA**

Our training dataset is compromised of 5 columns: 'uniqueID', 'classLabel', 'classID', 'source', 'imageFile'. The two columns 'classLabel', 'classID' correspond to the label we will be predicting. The 'source' column is what organization it came from. This can hold some correlation that we can explore-- like if more microscopic specimens come from a certain laboratory/foundation etc. more than others within 'sources'.

**Correlation** is a statistical measure that expresses the extent to which two variables are linearly related. In our example, if a source provides a significantly larger number of samples compared to the other sources for a specific class, you can say there is a correlation-- a strong association between that source and class. 

Here is the breakdown of the classes: <img width="414" alt="image" src="https://github.com/user-attachments/assets/1d28f887-bf64-445c-ae91-642c4b59482e">

We can create a countplot to visualize the contributions per source
<img width="837" alt="image" src="https://github.com/user-attachments/assets/24eb6cab-1af1-41d3-aa2a-08226dda3dbc">

This isn't as easy to read so we can look at individual class labels:

And after looking at one of the labels, 'microscope-slides', we can see that of the 37 different sources, only 3 contribute microscope slides with the majority provided by 'L'.
<img width="727" alt="image" src="https://github.com/user-attachments/assets/a9672a0a-ff38-4be1-9c79-66e8c703461a">

Same with 'illustrations-color' with the majority sourced by 'BHL'
<img width="736" alt="image" src="https://github.com/user-attachments/assets/eb6e1f40-fad6-44ac-a61f-e986d316c034">

Or we can look at the first half of the sources that have most variation and/or samples from the training data.
![image](https://github.com/user-attachments/assets/7af1a881-4492-4c41-96a2-5f02fdb152fe)

Still not the best but it's a way to see if there is correlation within the source column and a specific class and there seems to be for some. 

- [X] Exploratory Data Analysis
- [ ] Model Creation
- [ ] Hyperparameter Tuning
- [ ] Performance


## **Model Creation** 
For our model, we are using a pretrained Xception model via Keras for the image classification. Xception by Google, stands for Extreme version of Inception. We previously tried VGG16, K Nearest Neighbors, Yolo, ---- and found that it was either too computationally exhaustive, wasn't accurate, or ...

### Xception Model
Standard convolution (cnn) learns filters in 3D space, with each kernel learning width, height, and channels.

Whereas, a depthwise separable convolution (Xception) divides the process into two distinctive processes using depth-wise convolution and pointwise convolution:

Depthwise Convolution: Here, a single filter is applied to each input channel separately. For example, if an image has three color channels (red, green, and blue), a separate filter is applied to each color channel.

Pointwise Convolution: After the depthwise convolution, a pointwise convolution is applied. This is a 1×1 filter that combines the output of the depthwise convolution into a single feature map.

<img width="629" alt="Screenshot 2024-09-28 at 7 13 30 PM" src="https://github.com/user-attachments/assets/3eff57bc-a71c-400b-b904-f88791545931">

https://keras.io/api/applications/xception/

- [X] Exploratory Data Analysis
- [X] Model Creation
- [ ] Hyperparameter Tuning
- [ ] Performance


## **Tuning**
The Xception model has the same number of parameters as Inception model.

- **include_top:** whether to include the 3 fully-connected layers at the top of the network.
- **weights:** one of None (random initialization), "imagenet" (pre-training on ImageNet), or the path to the weights file to be loaded.
- **input_tensor:** optional Keras tensor (i.e. output of layers.Input()) to use as image input for the model.
- **input_shape:** optional shape tuple, only to be specified if include_top is False (otherwise the input shape has to be (299, 299, 3). It should have exactly 3 inputs channels, and width and height should be no smaller than 71. E.g. (150, 150, 3) would be one valid value.
- **pooling:** Optional pooling mode for feature extraction when include_top is False.
None means that the output of the model will be the 4D tensor output of the last convolutional block.
avg means that global average pooling will be applied to the output of the last convolutional block, and thus the output of the model will be a 2D tensor.
max means that global max pooling will be applied.
- **classes:** optional number of classes to classify images into, only to be specified if include_top is True, and if no weights argument is specified.
- **classifier_activation:** A str or callable. The activation function to use on the "top" layer. Ignored unless include_top=True. Set classifier_activation=None to return the logits of the "top" layer. When loading pretrained weights, classifier_activation can only be None or "softmax".
- **name:** The name of the model (string).

```
base_model = Xception(
    weights='imagenet',
    include_top=False, 
    classifier_activation='softmax'
    )
  ```
We set the weights to 'imagenet' for the pretrained model. The include_top=False sets model to output features from the last convolutional block instead of class probabilities. Then we'll set input/outputs and run a Keras base model.

- [X] Exploratory Data Analysis
- [X] Model Creation
- [X] Hyperparameter Tuning
- [ ] Performance

## **Performance**

After hyperparameter tuning and many epochs, here is out performance after 10 epochs ```loss: 0.0312 - accuracy: 0.9444 - val_loss: 0.0289 - val_accuracy: 0.9463```. And this was after we froze some layers of the model and updated others. It only led to a 0.04 increase in accuracy but stayed resistant to overfitting.


- [X] Exploratory Data Analysis
- [X] Model Creation
- [X] Hyperparameter Tuning
- [X] Performance
