# Documentation of Assignment

## Submission Details

- **Name**: Abhinav Anurag
- **Institution**: IIT Bombay
- **Email**: abhinav70291@gmail.com

## Overview

This code is designed to work with various models from the `torchvision.models.detection` module. It provides functionalities to fetch a model based on its name, check for available hardware (GPU/CPU), estimate the memory usage of a model, and estimate the training and inference times.

## System Design

The system is designed with simplicity and modularity in mind. It is divided into four main functions:

1. `get_model(model_name, pretrained=True, device='cpu')`
2. `get_device()`
3. `get_model_memory_usage(batch_size, model)`
4. `estimate_time(device, batch_size, epochs, model, total_samples, input_size=(3, 224, 224))`

### `get_model(model_name, pretrained=True, device='cpu')`

This function fetches a model based on its name. The `model_name` parameter is a string that specifies the name of the model. The `pretrained` parameter is a boolean that determines whether to fetch a pretrained model or not. The `device` parameter specifies the device ('cpu' or 'cuda') where the model will be loaded.

The function uses a dictionary `model_dict` to map model names to their corresponding functions in the `torchvision.models.detection` module. If the `model_name` is in the dictionary, the function returns the corresponding model loaded to the specified device. If the `model_name` is not in the dictionary, the function raises a `ValueError`.

### `get_device()`

This function checks if a GPU is available. If a GPU is available, it returns `torch.device('cuda')`. If a GPU is not available, it returns `torch.device('cpu')`.

### `get_model_memory_usage(batch_size, model)`

This function estimates the memory usage of a model. The `batch_size` parameter is an integer that specifies the batch size. The `model` parameter is a PyTorch model.

The function calculates the memory usage of the model’s features and parameters separately, then adds them together to get the total memory usage. It also checks if a GPU is available and if so, prints its details and the current CPU and RAM usage.

### `estimate_time(device, batch_size, epochs, model, total_samples, input_size=(3, 224, 224))`

This function estimates the training and inference times. The parameters are `device` (the device where the model is loaded), `batch_size` (the batch size), `epochs` (the number of epochs), `model` (the PyTorch model), `total_samples` (the total number of samples), and `input_size` (the size of the input tensor).

The function creates a random input tensor on the CPU, moves it to the specified device, and feeds it to the model. It measures the time taken for both the forward pass and the backward pass( assuming that backward pass time is roughly equal to the forward pas) , and uses these times to estimate the total training and inference times.

## Parameters

The code uses several parameters to control its behavior:

### `device`

The `device` parameter is obtained by calling the `get_device()` function. This function checks if a GPU is available and returns `torch.device('cuda')` if it is. If a GPU is not available, it returns `torch.device('cpu')`.

### `model_names`

The `model_names` parameter is a list of strings that specify the names of the models we're about to experiment with. The models are from the `torchvision.models.detection` module and include:

- 'maskrcnn_resnet50_fpn'
- 'fasterrcnn_resnet50_fpn'
- 'fcos_resnet50_fpn'
- 'retinanet_resnet50_fpn'
- 'ssd300_vgg16'
- 'ssdlite320_mobilenet_v3_large'

### `batch_size`
In this case, the batch size is set to 8.

### `epochs`
In this case, the number of epochs is set to 3.

### `total_samples`

The `total_samples` parameter is an integer that specifies the total number of samples in your dataset. In this case, the total number of samples is set to 50,000. You should replace this with the actual size of your dataset.

These parameters are used throughout the code to control the behavior of the model, the hardware used, and the training process. They are designed to be easily adjustable to suit your specific needs.


## Conclusion

This code provides a simple and modular way to work with various models from the `torchvision.models.detection` module. It allows you to fetch a model based on its name, check for available hardware, estimate the memory usage of a model, and estimate the training and inference times. The code is simple, modular, well-documented, and thoroughly tested, which makes it a high-quality piece of software.
