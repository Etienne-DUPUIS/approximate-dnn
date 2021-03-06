# Approximate Computing in Deep Neural Networks

Hoping to give a clear view on the subject with curated contents organized

From algorithm to hardware execution

- [Approximate Computing in Deep Neural Networks](#approximate-computing-in-deep-neural-networks)
  * [Lexical](#lexical)
  * [Best Surveys](#best-surveys)
  * [Tools](#tools)
    + [Approximations Frameworks](#approximations-frameworks)
    + [Dedicated Library](#dedicated-library)
    + [Graph Compiler](#graph-compiler)
    + [Dedicated HW (ASIC)](#dedicated-hw--asic-)
    + [FPGA based accelerator](#fpga-based-accelerator)
    + [Evaluation Frameworks](#evaluation-frameworks)
  * [Approximation Methods](#approximation-methods)
    + [Pruning](#pruning)
      - [Unstructured](#unstructured)
      - [Structured - Sub-kernel](#structured---sub-kernel)
      - [Structured - Kernel](#structured---kernel)
      - [Structured - Filter](#structured---filter)
      - [Structured - Hardware Friendly Structure](#structured---hardware-friendly-structure)
      - [Weight Saliency Determination](#weight-saliency-determination)
    + [Quantization](#quantization)
    + [Approximate operators](#approximate-operators)
  * [Others](#others)
    + [Optimization Framework](#optimization-framework)
    + [DNN conversion framework](#dnn-conversion-framework)
    + [Simulation Framework](#simulation-framework)
    + [Visualization Framework](#visualization-framework)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>





## Lexical

- PQT: Post Training Quantization
- QAT: Quantization Aware Training


## Best Surveys

- 2019 [Deep Neural Network Approximation for Custom Hardware:Where We’ve Been, Where We’re Going](https://arxiv.org/abs/1901.06955), Wang & al.
- 2017 [Efficient Processing of Deep Neural Networks: A Tutorial and Survey](https://ieeexplore.ieee.org/document/8114708), Sze & al.
- 2020 [Model Compression and Hardware Acceleration for Neural Networks: A Comprehensive Survey](http://ieeexplore.ieee.org/document/9043731), Deng & al.
- 2020 [Approximation Computing Techniques to Accelerate CNN Based Image Processing Applications – A Survey in Hardware/Software Perspective](https://www.researchgate.net/publication/342754132_Approximation_Computing_Techniques_to_Accelerate_CNN_Based_Image_Processing_Applications_-_A_Survey_in_HardwareSoftware_Perspective), Manikandan & al.

## Tools

### Approximations Frameworks
| Name | Description | Framework | Supported Approx|
|---|---|---|---|
| [NEMO](https://github.com/pulp-platform/nemo) | small library for minimization of DNNs intended for ultra low power devices like pulp-nn | PyTorch, ONNX | PQT, QAT|
| [NNI](https://github.com/microsoft/nni) | lightweight toolkit for Feature Engineering, Neural Architecture Search, Hyperparameter Tuning and Model Compression | Pytorch, Tensorflow (+Keras), MXnet, Caffe2 CNTK, Theano | Pruning / PQT)|
| [PocketFlow](https://github.com/Tencent/PocketFlow) | open-source framework for compressing and accelerating DNNs. | Tensorflow | PQT, QAT, Prunning |
| [Tensorflow Model Optimization](https://github.com/tensorflow/model-optimization/) | Toolkit to optimize ML / DNN model | Tenforflow(Keras) | Clustering, Quantization (PQT, QAT), Pruning |
| [Brevitas](https://github.com/Xilinx/brevitas) | Pytorch extension to quantize DNN model | Pytorch | PQT, QAT | 

### Dedicated Library

- PULP-NN [code](https://github.com/pulp-platform/pulp-nn), [paper](https://arxiv.org/abs/1908.11263) - QNN inference library for ultra low power PULP RiscV core

### Graph Compiler

- [DORY](https://github.com/pulp-platform/dory) - automatic tool to deploy DNNs on low-cost MCUs with typically less than 1MB of on-chip SRAM memory
- [Glow](https://github.com/pytorch/glow) - Glow is a machine learning compiler and execution engine for hardware accelerators (Pytorch, ONNX) 
- [TensorflowLite](https://www.tensorflow.org/lite/guide) - TensorFlow Lite is a set of tools to help developers run TensorFlow models on mobile, embedded, and IoT devices. It enables on-device machine learning inference with low latency and a small binary size (linux, android, mcu). [curated content for tflite](https://github.com/margaretmz/awesome-tensorflow-lite)
- [OpenVino](https://docs.openvinotoolkit.org) - OpenCL based graph compiler for intel environnment (Intel CPU, Intel GPU, Dedicated accelerator)

### Dedicated HW (ASIC)
| Name | Description | Environment | Perf |
|---|---|---|---|
|[Esperanto ET-soc-1](https://www.esperanto.ai/esperanto-technologies-to-reveal-chip-with-1000-cores-at-risc-v-summit/) | 1000+ low power risc v core chip energy efficient processing of ML/DNN | Cloud | 800 TOPS @ 20W |
|[Google TPU](https://cloud.google.com/tpu/docs/tpus) | Processing unit for DNN workload, efficient systolic array for computation | Cloud, Edge | V3 - 90 TOPS @250W, Coral Edge 4TOPS @ 2W |
|[Greenwave GAP8](https://ieeexplore.ieee.org/document/8445101)| multi-GOPS fully programmable RISC-V IoT-edge computing engine, featuring a 8-core cluster with CNN accelerator, coupled with an ultra-low power MCU with 30 μW state-retentive sleep power (75mW)|Edge| 600 GMAC/s/W|

### FPGA based accelerator

- [Maestro](https://github.com/maestro-project/maestro) - open-source tool for modeling and evaluating the performance and energy-efficiency of different dataflows for DNNs
- [HLS4ML](https://github.com/fastmachinelearning/hls4ml) - package for creating HLS from various ML framework (good pytorch support), create streamline architecture
- [FINN](https://github.com/Xilinx/finn) - framework for creating HW accelerator (HLS code) from BREVITAS quantized model, downto BNN, create PE architecture
- [N2D2](https://github.com/CEA-LIST/N2D2) - framework for creating HLS from N2D2 trained model (support ONNX import), create streamline architecture

### Evaluation Frameworks

- [DNN-Neurosim](https://github.com/neurosim/DNN_NeuroSim_V2.0) - Framework for evaluating the performance of inference or training of on-chip DNN



## Approximation Methods

- 2020 [Deep Neural Network Compression by In-Parallel Pruning-Quantization](https://ieeexplore.ieee.org/document/8573867) - Use Bayesian optimization to solve both pruning and quantization problems jointly and with fine-tuning.

- 2020 [OPQ: Compressing Deep Neural Networks with One-shot Pruning-Quantization](https://www.semanticscholar.org/paper/OPQ%3A-Compressing-Deep-Neural-Networks-with-One-shot-Hu-Peng/7b16367b575d951a98f1762d8f45d7c0eb840581) - Analytical single shot compression (Pruning + Quantization) of DNN using only pretrained weights values, then fine-tuning to recover ACL 

### Pruning

#### Unstructured

#### Structured - Sub-kernel

#### Structured - Kernel

#### Structured - Filter

#### Structured - Hardware Friendly Structure

- [Accelerating Sparse DNN Models without Hardware-Support via Tile-Wise Sparsity](https://arxiv.org/pdf/2008.13006.pdf) - Large matrix multiplication are tiled, this method propose to maintain a regular pattern at the tile level, improving efficiency.

#### Weight Saliency Determination

- 2020 [Utilizing Explainable AI for Quantization and Pruning of Deep Neural Networks](https://arxiv.org/abs/2008.09072) - Using DeepLift (explainable AI) as hints to improve compression by determining importance of neurons and features

### Quantization

- 2018 [Learning Compression from Limited Unlabeled Data](https://openaccess.thecvf.com/content_ECCV_2018/papers/Xiangyu_He_Learning_Compression_from_ECCV_2018_paper.pdf) - Use unlabelled data to improve accuracy of quantization in a very fast fine-tuning step

### Approximate operators
- 2020 [Full Approximation of Deep Neural Networks through Efficient Optimization](https://ieeexplore.ieee.org/document/9181236/) - Select efficient approx multipliers through retraining and minimization of accuracy loss (Evo Approx)
- 2019 [ALWANN: Automatic Layer-Wise Approximation of Deep Neural Network Accelerators without Retraining](https://arxiv.org/abs/1907.07229) - Use NSGA II to optimize approximate multipliers implemented & DNN mapping onto implemented Ax multipliers (Evo Approx).


## Others

### Optimization Framework

- [Google OR-Tools](https://developers.google.com/optimization/introduction/overview)

### DNN conversion framework

- [MMdnn](https://github.com/Microsoft/MMdnn) - Microsoft tool for cross-framework conversion, retraining, visualization & deployment
- [ONNX](https://github.com/onnx/onnx) - model format to exchange frozen models between ML frameworks 
### Simulation Framework

- [Renode](https://github.com/renode/renode) - Simulation platform for MCU dev & test (functional, single and multi-node)

### Visualization Framework

- [Tensorboard](https://www.tensorflow.org/tensorboard) - Visualization tool for Tensorflow, Pytorch ..., can show graph, metric evolution over training ... very adaptable
- [Netron](https://github.com/lutzroeder/netron) - Tool to show ONNX graph with all the attributes.
