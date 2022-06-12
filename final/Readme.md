# **Abstract**
## To solve medical segmentation problem about spread through air spaces(STAS),we construct a Unet model with attention block followed by decoder,whose encoder is EfficientNetB3.In addition,we use another model called Feature Pyramid Network(FPN) to complete our work.We also use data augmentation technique to generalize our model capability.The training f1score is 0.86 ± 0.005.The future work we will try to add Atrous Spatial Pyramid Pooling （ASPP）technique or try Unet3plus architecture to get better result.The other future work is post-processing. 

# **1.PACKAGE**
### Python == 3.7.13
### torch == 1.11.0
### numpy == 1.21.6
### Pillow == 7.1.2
### Scikit-learn == 1.0.2
### OpenCV == 4.1.2.30
### albumentations == 0.1.12
### segmentation-models-pytorch == 0.2.1
### inplace-abn == 1.1.0

# **2.Directory**
### due to use of colab,the file directory needs modifying in Section Load & Process Data 
![image.png](data:image/png;base64,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)

# **3.Data Augmentaion Block**
### make sure that we have albumentations packages,or you can use this command:
### **install -U git+https://github.com/albu/albumentations --no-cache-dir**

# **4.Create Model**
### make sure that we have segmentation-models-pytorch packages,or you can use this command:
### **pip install segmentation-models-pytorch**

### we provide two option to construct model.One is Unet with attention technique and the other is FPN model which use all decoder layers to predict output while the previous one is the last decoder layer to predict output.Furthermore,we alse provide inplace-abn option to save the memory used.Make sure that we have inplace-abn packages,or you can use this command:
### **pip install inplace-abn**

# **5.Reference**
### http://jase.tku.edu.tw/articles/jase-202212-25-6-0012
### https://arxiv.org/abs/1910.08978
### https://arxiv.org/abs/1505.04597
### https://openaccess.thecvf.com/content_cvpr_2017/papers/Lin_Feature_Pyramid_Networks_CVPR_2017_paper
### https://arxiv.org/pdf/1712.02616.pdf



```python

```