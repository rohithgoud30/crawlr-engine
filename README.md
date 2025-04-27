# Crawlr Engine - Notebook Crawler

A Jupyter Notebook script to crawl websites from the Majestic Million list and call local API endpoints to find Terms of Service and Privacy Policy pages.

## Features

- Downloads Majestic Million CSV.
- Processes domains sequentially by rank.
- Calls local API endpoints (`/legal/crawl/terms-of-service`, `/legal/crawl/privacy-policy`).
- Uses checkpointing to resume from interruption.
- Tracks and displays statistics (success/failure counts, percentages, runtime).
- Avoids processing duplicate domains.

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

3.  **Prepare API Server:**
    Ensure your backend server (providing the `/legal/crawl/...` endpoints) is running, typically on `http://127.0.0.1:8000`.

4.  **Run Jupyter Notebook:**
    ```bash
    jupyter notebook crawler.ipynb
    ```

## Usage

- Open `crawler.ipynb` in Jupyter.
- Verify the `API_BASE_URL`, `ENDPOINTS`, and `API_KEY` in the configuration cell match your running server setup.
- Run the cells sequentially.
- The script will download the CSV, process domains, call the API, and save progress.
- Statistics are printed periodically and at the end.
- If interrupted (e.g., Ctrl+C), the script saves its state and can be resumed by running the main execution cell again.
