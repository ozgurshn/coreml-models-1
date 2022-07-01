### Convert MobileBERT_SQuAD to Core ML

Worked version is trial 2.


#### Trial 1:

Convert SavedModel to Core ML.

Failed with error:
```
ValueError: Importing a SavedModel with tf.saved_model.load requires a 'tags=' argument if there is more than one MetaGraph. Got 'tags=None', but there are 2 MetaGraphs in the SavedModel with tag sets [['serve'], ['serve', 'tpu']]. Pass a 'tags=' argument to load this SavedModel.
```

#### Trial 2:

Convert SavedModel to ConcreteFunction then convert ConreteFunction to Core ML.

**Quantization**:
16 bits worked, but 8 bits quantized model failed to load later in iOS with error:

```
/Library/Caches/com.apple.xbs/Sources/MetalImage/MetalImage-124.2.4/MPSCore/Types/MPSMatrix.mm, line 222: error '[MPSMatrix initWithBuffer:descriptor:] not enough rowBytes for all the columns.'
/Library/Caches/com.apple.xbs/Sources/MetalImage/MetalImage-124.2.4/MPSCore/Types/MPSMatrix.mm:222: failed assertion `[MPSMatrix initWithBuffer:descriptor:] not enough rowBytes for all the columns.'
```

#### Trial 3:

Try to optimize the TF graph then save as SavedModel.

Failed with error:
```
ValueError: Input 0 of node Cast was passed float from input_mask:0 incompatible with expected int32.
```
