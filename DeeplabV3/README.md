### Convert DeeplabV3_ADE20K to Core ML

#### Trial 1:

The model can be converted successfully and produces plausible result without modifying
any layers. But the latency is very high, about 790 ms per frame on iPhone Xs.

#### Trial 2:

Try to optimize the TF graph before conversion by striping unused nodes. But failed in to
convert from TF to Core ML with error:

```
ValueError: Input 0 of node Shape was passed float from ImageTensor:0 incompatible with expected uint8.
```

#### Trial 3:

The model can be converted successfully and produces plausible result without modifying
any layers. Model is quantized to 8 bits. On iPhone Xs, latency reduced from 790 ms (no
quantization) to 220 ms.

#### Trial 4:

The model is quantized to 8 bits. On iPhone Xs, latency reduced from 790 ms (no quantization)
to 220 ms. Using tfcoreml to optimize the TF graph, the latency reduced further to 150 ms.

Note: tfcoreml rebuild the TF graph then use coremltools to convert to Core ML format.

#### Trial 5:

Use `MobilenetV2/MobilenetV2/input` instead of `ImageTensor` as input. The latency is the same as trial 4.

