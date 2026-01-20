# Lakeflow-Using-Public-API

A starter project to interact with the Lakeflow public API. This repository contains a minimal Python client, a basic project layout, tests, and a CI workflow to help you get started.

## Quickstart

1. Create a virtual environment and activate it:

   macOS / Linux
   ```
   python -m venv .venv
   source .venv/bin/activate
   ```

   Windows (PowerShell)
   ```
   python -m venv .venv
   .venv\Scripts\Activate.ps1
   ```

2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Run tests:
   ```
   pytest -q
   ```

4. Example usage (see `src/lakeflow_client.py` for details):
   ```py
   from src.lakeflow_client import LakeflowClient

   client = LakeflowClient(api_key="YOUR_API_KEY", base_url="https://api.lakeflow.example")
   data = client.get_resource("/v1/resources/123")
   print(data)
   ```

## Contributing

Please open issues or pull requests. Follow the existing code style and add tests for new features.

## License

This project is offered under the MIT License. See LICENSE for details.
