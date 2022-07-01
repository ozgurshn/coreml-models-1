### SSD MobileNet V2 to Core ML

#### Trial 1:

Try using TF2 to convert saved model to Core ML. Failed with error:

```
ValueError: Unable to determine the shape of input: unused_control_flow_input_13. Please provide its shape during conversion, using 'ct.convert(..., inputs=[ct.TensorType(name='unused_control_flow_input_13', shape=(_FILL_ME_) ),])
```

#### Trial 2:

Try using TF1 to convert from frozen graph to Core ML. Failed with error:

```
NotImplementedError: Conversion for TF op 'Rank' not implemented.
```

#### Trial 3:

Try using TF2 to convert from saved model to Core ML with given input and output names.
Failed with error:

```
ValueError: Graph is not a DAG!
```

#### Trial 4:

Try using TF1 to convert from saved model to Core ML with given input and output names.
Failed with error:

```
NotImplementedError: Conversion for TF op 'Rank' not implemented.
```

#### Trial 5:

Try optimizing the TF graph befor conversion to Core ML. Failed with error:

```
ValueError: Input 0 of node ToFloat was passed float from image_tensor:0 incompatible with expected uint8.
```

#### Trial 6:

We use coremltools for conversion. The model is converted successful, but predict too many
bounding boxes.

Finally, using tfcoreml to convert from TF to Core ML then add additional layer for anchor
decoding and NMS, the converted Core ML model produce correct result.
