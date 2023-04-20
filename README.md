# node-red-flow-llama #

Node-RED Flow (and web page example) for the LLaMA AI model

This repository contains a function node for [Node-RED](https://nodered.org/) which can be used to run the [LLaMA model](https://ai.facebook.com/blog/large-language-model-llama-meta-ai/) using [llama.cpp](https://github.com/ggerganov/llama.cpp) within a Node-RED flow. **Inference is done on the CPU** and still completes within a few seconds on a reasonably powerful computer.

Having the actual inference as a self-contained function node gives you the possibility to define your own user interface or even use it as part of an autonomous agent.

> Nota bene: these flows do not contain the actual model. You will have to request your own copy directly from Meta AI using their official [Request Form](https://docs.google.com/forms/d/e/1FAIpQLSfqNECQnMkycAp2jP4Z9TFX0cGR4uf7b_fBxjY_OjhJILlKGA/viewform).

## Installation ##

The actual "heavy lifting" is done by [llama.cpp](https://github.com/ggerganov/llama.cpp). Simply follow the instructions found in section [Usage](https://github.com/ggerganov/llama.cpp#usage) to build the CLI command `main` for your platform.

Afterwards, rename `main` to `llama` and copy it into a subfolder called `ai` within the installation folder of your Node-RED server

### Preparing the Model ###

Once you got the actual LLaMA model, follow the instructions found in section [Prepare Data & Run](https://github.com/ggerganov/llama.cpp#prepare-data--run) to bring it into the proper format.

Afterwards, rename the file `ggml-model-q4_0.bin` to `ggml-llama-7b-q4.bin` and move (or copy) it into the same subfolder `ai` within the installation folder of your Node-RED server where you already placed the `llama` executable.

### Importing the Function Node ###

Finally, open the Flow Editor of your Node-RED server and import the contents of [LLaMA-Function.json](./LLaMA-Function.json). After deploying your changes, you are ready to run LLaMA inferences directly from within Node-RED.

## Usage ##

The prompt itself and any inference parameters have to be passed as properties of the msg object. The prompt is expected in `msg.payload` and will later be replaced by the result of the inference.

The following properties are supported:

* `payload` - this is the actual prompt 
* `seed` - 
* `threads` - 
* `context` - 
* `keep` - 
* `predict` - 
* `topk` - 
* `topp` - 
* `temperature` - 
* `batches` - 

All properties (except the prompt itself) are optional. If given, they should be strings (even if they contain numbers), this makes it simpler to extract them from an HTTP request.

## Example ##

The file [LLaMA-HTTP-Endpoint.json](./LLaMA-HTTP-Endpoint.json) contains an example which uses the LLaMA function node to answer HTTP requests. The prompt itself and any inference parameters have to be passed as query parameters, the result of the inference will then be returned in the body of the HTTP response.

The following parameters are supported (most of them will be copied into a `msg` property of the same name):

* `prompt` - will be copied into `msg.payload`
* `seed` - will be copied into `msg.seed`
* `threads` - will be copied into `msg.threads`
* `context` - will be copied into `msg.context`
* `keep` - will be copied into `msg.keep`
* `predict` - will be copied into `msg.predict`
* `topk` - will be copied into `msg.topk`
* `topp` - will be copied into `msg.topp`
* `temperature` - will be copied into `msg.temperature`
* `batches` - will be copied into `msg.batches`

In order to install this flow, simply open the Flow Editor of your Node-RED server and import the contents of [LLaMA-HTTP-Endpoint.json](./LLaMA-HTTP-Endpoint.json)

### Web Page ###

The file [LLaMA.html](./LLaMA.html) contains a trivial web page which can serve as a user interface for the HTTP endpoint. Ideally, this page should be served from the same Node-RED server that also accepts the HTTP requests for LLaMA, but this is not strictly necessary.

> Nota bene: **inference is still done on the Node-RED server**, not within your browser!

## License ##

[MIT License](LICENSE.md)
