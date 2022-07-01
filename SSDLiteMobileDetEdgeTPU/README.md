### Convert SSDLiteMobileDetEdgeTPU to Core ML

#### Trial 1:

Failed to open the TF frozen graph because FusedBatchNormV3 is used but not supported in
TF1

#### Trial 2:

Failed to inspect the frozen_graph because TFLite_Detection_PostProcess is not supported
by normal TensorFlow verison.

Failed to convert to Core ML because coremltools can not open frozen graph if TF2 is used.

#### Trial 3:

Using TF2, convert the frozen graph to saved model, then convert the saved mode to Core
ML, then add layer for anchors decoding and NMS. The conversion is successful but the
prediction result is not correct.