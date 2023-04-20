# node-red-flow-llama #

Node-RED Flow (and web page example) for the LLaMA AI model

This repository contains a function node for [Node-RED](https://nodered.org/) which can be used to run the [LLaMA model](https://ai.facebook.com/blog/large-language-model-llama-meta-ai/) using [llama.cpp](https://github.com/ggerganov/llama.cpp) within a Node-RED flow. **Inference is done on the CPU** and still completes within a few seconds on a reasonably powerful computer.

Having the actual inference as a self-contained function node gives you the possibility to define your own user interface or even use it as part of an autonomous agent.

> Nota bene: these flows do not contain the actual model. You will have to request your own copy directly from Meta AI using their official [Request Form](https://docs.google.com/forms/d/e/1FAIpQLSfqNECQnMkycAp2jP4Z9TFX0cGR4uf7b_fBxjY_OjhJILlKGA/viewform).

## Installation ##

## Usage ##

The prompt itself and any inference parameters have to be passed as properties of the msg object. The following properties are supported:

* payload
* seed
* threads
* context
* keep
* predict
* topk
* topp
* temperature
* batches

## Example ##

The file [LLaMA-HTTP-Endpoint.json](./LLaMA-HTTP-Endpoint.json) contains an example which uses the LLaMA function node to answer HTTP requests. The prompt itself and any inference parameters have to be passed as query parameters. The following parameters are supported

* prompt
* seed
* threads
* context
* keep
* predict
* topk
* topp
* temperature
* batches

## License ##

[MIT License](LICENSE.md)
