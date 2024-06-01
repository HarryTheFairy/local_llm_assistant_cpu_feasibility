# local_llm_assistant_cpu_feasibility

## Main goal
Using a large language model to understand and help with technical documentation.
Looking features like:
* Chatbot for asking questions about existing documenation (apparently called RAG for retreival augmented generation)
* Retreiving specific information
* Provide suggestions while writing new documenation. Mentioning if the same meaning is already writing somewhere or suggest linking to existing related topics.
* Maybe even guess what readers of the documentation might expect but is missing, providing questions and answers that could be added.
* Understand scripting languages. / Scripts in python and Matlab
* Generate alterations of existing scripts based on chat instructions. (These scripts are not too complicated but have several variants too them which are hard to rememeber and some common mistakes which need to be prevented)
* (optional) maybe help with task tracking and planning strategies on how to proceed. But apperantly current models are quite bad at that.
* Run locally without any cloud services (mandatory for personal and confidential notes and documentation)
* Run on Intel 13th gen CPU with <=32GB RAM without dedicated GPU
* Free and open source. There is a lot available so why not use that first? Interesting if this can be used by anybody at work without caring about licensing fees.

## Non-goals
* No need to be superfast. A little latency is not an issue but I do not want to wait >1 minute for a short answer.
* No need to train. Testing may show otherwise but hopefully pretrained models are good enough understand existing text and deliver outputs for a RAG application
* No need for multimodal. Although it would be extremely nice for the model to only understand the text but also the graphics within a document (as there are many and graphics are very useful to tell a story) this is definately way to much too ask of a mobile CPU. Voice/Dictation would be also interesting but this can probably be done in a seperate speech to text process aswel. Future hardware releases with Mobile CPUs that have TPUs/NPUs integrated may change this a bit in the next years.

## Existing projects / tools
### Reor
https://github.com/reorproject/reor
Note taking application, aiming to use local models for understanding, organizing and chatting with local notes.
Relatively new and I did not see a lot of Articles using and evaluating this tool.
Maybe a very good option but need to wait for later releases.
## Model infrastructure
"Running" the model on your system. Creating a process/server which can be interacted with via command line and API.
### ollama
https://github.com/ollama/ollama
Very commonly mentioned tool for retreiving models and chatting with them.
But it seems this is the default when building applications with graphics cards. I did not see an example yet that runs good on CPU only.
For CPU only llama.cpp is often mentionend as alternative
### llama.cpp
https://github.com/ggerganov/llama.cpp
llama.cpp seems to be THE project to use for running models locally on CPU without GPU. Giving greedy and lazy tool enthusiasts the possibility to demand futuristic intelligence barely good enough corporate hardware. Builtin NPU/TPU might support this cause in the near future.
This is very good to at least get some experience even with low tokens per second, because buying any hardware right now looks so risky since its expected to be out of date very quickly when new ASICS come to the market.

## Models
Since compute and RAM is very limited by the hardware requirements I am mostly looking into 7B and 8B models or similae.
### Llama3 8B
* github: https://github.com/meta-llama/llama3
* huggingface full model: https://huggingface.co/meta-llama/Meta-Llama-3-8B-Instruct
* huggingface for llama.cpp with different quantizations: https://huggingface.co/QuantFactory/Meta-Llama-3-8B-Instruct-GGUF 
Seems to be a very good option for semantic understanding of text and also for coding. And open source. Seems to be the default target for llama.cpp (although its llama2 in most examples for now but llama3 is fresh and probably just needs to worked on).
Many different quantization version available on huggingface without needed any manual converstion steps.
This sounds ideal.
### Zephyr 7B
https://github.com/inferless/Zephyr-7b-beta
Mentioned here because it seem to be one of the default model options in reor project. I do not know yet why.
Seems to be base on Mistral 7B model and fine tuned as assistant. 
I am not sure how important this fine tuning might be because when using llama3 the way it answers seems to be mostly ok and less wordy than many chatbots which is ok for technical documentation and automation. It does not need to be a pretty and polite output, just as accurate and efficient as possible.
### Mistral 7B
https://huggingface.co/mistralai/Mistral-7B-v0.1
A open source model which apparently is quite good for its size and uses a different architecture. I saw it in use for several automation assistans in some projects. May be interesting to test it against llama3 8B
## LLM Terms
### Quantization
A technique which enables to run models with less powerful compute while sacrificing accuracy.
Running full model on a mobile CPU with 32GB RAM does not perform well. Quantized models are hopefully a solution to cheap out on hardware while still being accurate enough to understand existing documentation.
### Parameters 
Number of parameters is also often called the "size of the model".
More parameters generally means better understanding of complex patterns but depending on other factors like architecture, weights, training data quality and more smaller models can also be significantly better in certain tasks compared to larger models.
More parameters allways means higher computational requirements.
The limit for mobile CPU with 32GB or RAM model should be around 7B to 13B parameters (most likely needs quantization)
### 

Instead of using the readme file all these notes may go into a github page instead, but I am not entirely sure yet what that is..
If there are any comments, corrections, or suggestion for existing projects which already do that kind of stuff I am happy to hear it.



