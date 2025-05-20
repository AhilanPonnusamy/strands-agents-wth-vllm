# Details about this POC can be found in this [blog](https://github.com/AhilanPonnusamy/strands-wth-vllm/edit/main/README.md)

1. Setup local vLLM instance following the steps provided [here](https://github.com/AhilanPonnusamy/llm-cag-cpu). Start the vLLM instance with the required parameters and with your model of choice as shown below (adjust for GPU deployments as needed) 

```bash
export VLLM_CPU_KVCACHE_SPACE=16 # KV Cache in GBs
export HF_TOKEN=hf_xxxxxxxxxxxxxxxxxxxxxx  # Replace with your Hugging Face token

VLLM_USE_CUDA=0 python -m vllm.entrypoints.openai.api_server \
  --model Qwen/Qwen3-4B \
  --dtype float32 \
  --max-model-len 16384 \
  --max-num-seqs 1 \
  --swap-space 8 \
  --disable-sliding-window \
  --enable-prefix-caching \
  --enable-auto-tool-choice \
  --tool-call-parser llama3_json \
  --hf-token $HF_TOKEN 
```
   
2. Download the code repository with vLLM Model Provider implementation (install git if it is not already setup, You can also downlod the zip file directly from the main page under code option as an alternate)

```
brew install git
git clone https://github.com:AhilanPonnusamy/sdk-python.git
```

3. Ensure you have Python 3.10+ installed, then:

```bash
# Create and activate virtual environment
python -m venv strands-venv
source strands-venv/bin/activate  # On Windows use: strands-venv\Scripts\activate

# Install Strands and tools
pip install strands-agents strands-agents-tools
```
4. From **sdk-python** folder, setup local development environment following the **Development Envrionment** section available [here](https://github.com/strands-agents/sdk-python/blob/main/CONTRIBUTING.md) (Required to use vLLM Model Provider)
   
5. Create a python script called **vllm-example.py** with the following code
```bash
from strands import Agent
from strands.models.vllm import VLLMModel

# vLLM
vllm_model = VLLMModel(
  host="http://localhost:8000",
  model_id="Qwen/Qwen3-4B"
)
agent_vllm = Agent(model=vllm_model)
agent_vllm("Tell me about Agentic AI")

```
6. Execute the script to see stands-agents in action
```
python vllm-example.py
```
7. To see tools at work, create another python script called **vllm-agent-example.py** with the following code
```bash
from strands import Agent
from strands.models.vllm import VLLMModel
from strands_tools import current_time

# vLLM
vllm_modal = VLLMModel(host="http://localhost:8000", model_id="Qwen/Qwen3-4B")
agent_vllm = Agent(model=vllm_modal,tools=[current_time])
agent_vllm("What is the current time in Melbourne Australia?")
```
8. Execute the script to see tools in action
```bash
python vllm-agent-example.py
```
🎉 **Have Fun! Extend, explore, and enjoy!** 😄
   


