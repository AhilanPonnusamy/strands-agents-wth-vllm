# Details about this POC can be found in this [blog](https://github.com/AhilanPonnusamy/strands-wth-vllm/edit/main/README.md)

1. Setup local vLLM instance following the steps provided [here](https://github.com/AhilanPonnusamy/llm-cag-cpu)
   
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
4. Setup local development environment following the ##Development Envrionment## section available [here](https://github.com/strands-agents/sdk-python/blob/main/CONTRIBUTING.md)
