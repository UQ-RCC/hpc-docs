# AI and LLMs on Bunya
There are a variety of research workloads on Bunya working with artificial intelligence and machine learning. UQ RCC is working to establish and support these workloads with research integrity and security in mind.

### A note about commercial LLM services
Commercial LLM services that operate on external infrastructure such as Claude, ChatGPT, or GitHub Copilot are not permitted on Bunya.

## LLM inference tools
Currently, Bunya has the following tools available for performing local LLM inference:
* Ollama
* LLaMA.cpp
* vLLM

These tools can be used to run locally-stored models and provide command-line interfaces and an OpenAI-compatible API. LLaMA.cpp can also provide a web interface for use in e.g. a Firefox session in an onBunya desktop. An onBunya app to provide this interface without needing to launch a desktop session is in development and this guide will be updated when it is released.

Bunya also has Open-WebUI available, to act as a frontend to inference tools. It is available in the AI/ML menu in onBunya and by default will launch an Ollama server. You will be able to select a model to load from the Open-WebUI interface.

Models are stored in various directories in /scratch/opendata/models. You are encouraged to check the models available in there, as well as read the associated license files to ensure your usage follows the license agreement.

### Customised model usage
If you require fine control of the way the model loads and operates, you can load llama.cpp from the command line with `module load llama.cpp/cuda` for NVidia GPUs or `module load llama.cpp/rocm` for AMD GPUs. You can then run custom commands from that terminal. Ollama is provided in an Apptainer container, and you can see an example of how to run it by examining the file `/sw/containers/local/rcc/launch-scripts/ollama.sh`. You can use this file to start an Ollama server then run subsequent ollama commands via apptainer in the same way as used in that file.

## Code assistant
If you want to use LLMs for code assistance, this is supported in our onBunya VScode (code-server) app. If you launch a VScode session with a GPU, you can enable LLM assistance with this process:

* Launch a VScode session.
* Go to the extension marketplace (Open-VSX)
* Install Continue
* Once Continue is installed, copy the configuration file at `/sw/containers/local/rcc/ollama-continue/config.yaml` into the directory `~/.continue`.
* In the VScode terminal, run `module load ollama/continue` to start Ollama and preload the default models.
* If you subsequently change the models to something different, you can avoid preloading the default models by running `/sw/containers/local/rcc/launch-scripts/ollama.sh` instead.

The config file provided will set up Llama3:8b as your chat model, Deepseek-coder-v2:16b as your code assistant, and Nomic-embed-text as your text embedder. These are relatively small models with limited capabilities, but they will all fit simultaneously into a single A16 GPU so you will have access to functional tools with a minimum of waiting for the larger GPUs. You are welcome to change these to other models, and if Bunya does not currently have a model you need, contact RCC to have it installed.
