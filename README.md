# Crawlr Engine - Notebook Crawler

A Jupyter Notebook script to crawl websites from the Majestic Million list and call API endpoints to find Terms of Service and Privacy Policy pages.

## Features

- Downloads Majestic Million CSV.
- Processes domains sequentially by rank.
- Calls API endpoints for Terms of Service and Privacy Policy detection.
- Uses checkpointing to resume from interruption.
- Tracks and displays statistics (success/failure counts, percentages, runtime).
- Avoids processing duplicate domains.

## API Server Information

The crawler connects to the following API server:

- **Server URL**: `https://crwlr-server-662250507742.us-east4.run.app`
- **Terms of Service Endpoint**: `/api/v1/crawl-tos`
- **Privacy Policy Endpoint**: `/api/v1/crawl-pp`
- **API Key Requirement**: The server requires an API key for authentication (`X_API_KEY` header). Contact the project administrator to obtain your API key.

## Setup

1.  **Create and Activate Virtual Environment:**

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

2.  **Install Dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

3.  **Configure Environment Variables:**

    Copy the sample.env file to .env and update the endpoints:

    ```bash
    cp sample.env .env
    ```

    Edit the .env file to include:

    ```
    # API Configuration
    X_API_KEY=your_api_key_here  # Replace with your actual API key from the project admin

    # Endpoints
    TOS_ENDPOINT=https://crwlr-server-662250507742.us-east4.run.app/api/v1/crawl-tos
    PP_ENDPOINT=https://crwlr-server-662250507742.us-east4.run.app/api/v1/crawl-pp

    # Crawler Configuration
    TIMEOUT=10
    DELAY_BETWEEN_REQUESTS=1
    ```

    > **Note**: The `X_API_KEY` is required for authentication with the CRWLR server. Without a valid API key, the requests will be rejected with a 401 Unauthorized error. Please refer to the project documentation or contact the project administrator to obtain a valid API key.

4.  **Run Jupyter Notebook:**
    ```bash
    jupyter notebook crawler.ipynb
    ```

## Usage

- Open `crawler.ipynb` in Jupyter.
- Run the cells sequentially.
- When prompted, choose whether to crawl Terms of Service (1) or Privacy Policy (2).
- The script will download the CSV, process domains, call the API, and save progress.
- Statistics are printed periodically and at the end.
- If interrupted (e.g., Ctrl+C), the script saves its state and can be resumed by running the main execution cell again.
