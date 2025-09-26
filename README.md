# Chat app (Azure AI Foundry) — Python

This folder contains a simple generative AI chat client that connects to a model deployed in an Azure AI Foundry project. This README summarizes the steps from the lab instructions and adapts them for macOS / zsh.

> See the full exercise details at:
> https://microsoftlearning.github.io/mslearn-ai-studio/Instructions/02a-AI-foundry-sdk.html

## Prerequisites

- An Azure subscription with permission to create resources
- A model deployed in an Azure AI Foundry project (the lab uses `gpt-4o`)
- Azure CLI installed and available on your PATH (`az`)
- Python 3.11+ recommended

## Quick setup (macOS / zsh)

1. Clone the repo (if you haven't already):

```bash
git clone https://github.com/microsoftlearning/mslearn-ai-studio mslearn-ai-foundry
cd mslearn-ai-foundry/labfiles/chat-app/python
```

2. Create and activate a virtual environment named `labenv`:

```bash
python -m venv labenv
source labenv/bin/activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt azure-identity azure-ai-projects openai
```

> Note: `requirements.txt` in this folder contains core packages used by the lab. The explicit installs above ensure `azure-identity`, `azure-ai-projects` and `openai` are available.

## Configure the application

1. Edit the `.env` file in this folder and set the two variables:

```
PROJECT_ENDPOINT=<your-project-or-model-endpoint>
MODEL_DEPLOYMENT=<your-model-deployment-name>
```

- If you deployed the model in your project's default region you can use the project endpoint shown on the project Overview page.
- If the model was deployed to a different region (quota fallback), use the model-specific Target URI shown on the Models + Endpoints page.
- Typical model deployment name used in the lab: `gpt-4o`.

2. Save the file. This project is configured to read `PROJECT_ENDPOINT` and `MODEL_DEPLOYMENT` at runtime.

## Run the chat app

1. Sign into Azure (you must authenticate to use DefaultAzureCredential):

```bash
az login
```

2. Run the app:

```bash
python chat-app.py
```

3. When prompted, type a question (for example: "What is the fastest animal on Earth?").
- Use follow-up questions to keep the conversation context.
- Type `quit` to exit the program.

## Troubleshooting

- If you see authentication errors, ensure `az login` completed successfully and the account has access to the AI Foundry resource.
- If the model doesn't respond or you get rate-limit errors, wait a few seconds and try again — or verify model quota in your subscription/region.
- If the app raises exceptions about missing packages, verify the virtualenv is activated and re-run the pip install commands above.
- If you used a non-default region for the model, confirm you used the model Target URI (not the project Overview endpoint) in `.env`.

## Cleanup

Delete any Azure resources you created (resource group or project) to avoid charges. You can delete the resource group from the Azure Portal or use the CLI:

```bash
az group delete --name <your-resource-group> --no-wait --yes
```

## Notes

- This repository includes a `.gitignore` that excludes `.env` and the local virtual environment `labenv/` to avoid committing secrets and local environment files.
- Keep your `.env` (secrets) out of source control.
- The lab uses pre-release SDKs; behavior may change with newer SDK versions.