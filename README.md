# coreml-converter

Notebooks to convert TensorFlow models to Core ML.

The notebooks are created and meant to be run on Google Colab. All the dependencies needed are defined in the notebooks.

### Speed test results are tracked here:  

https://docs.google.com/spreadsheets/d/1v1Zhs-IlTV_arCiuvUWARAEWthnKfKNJU5WAGuo78UE/edit?usp=sharing


### Some general issues when trying to convert the TensorFlow models to Core ML are:

- coremltools can not read the TF model >> TF models need to convert to a format which coremltools can read (depend on TensorFlow version 1 or 2 are used)
- Ops are not supported by coremltools (e.g. TFLite_Detection_PostProcess, Rank, NonMaxSuppressionV5 , etc.) >> use another layers and implement the missing layers by adding additional layers to the model using coremltools
- Missing info about shape and data type after conversion >> add the missing info manually to core ml model
- Model successfully converted but run much slower than TFLite version >> identify which layers are not optimized for Core ML and try to replace those layers with similar layers


**Specific issues and errors can be viewed in the notebooks with suffix _trialX.ipynb**


### Helpful links:

- API Reference: https://apple.github.io/coremltools/index.html
- Core ML Specification: https://apple.github.io/coremltools/mlmodel/index.html
- Supported layers: https://github.com/apple/coremltools/blob/main/mlmodel/format/NeuralNetwork.proto (also see other *.proto files in the same directory)
