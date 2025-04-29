# Global-Co2-Emission-Visulaizer

# Flask Chatbot Backend & CO₂ Emission Dashboard GUI

This project contains two distinct Python applications bundled into a single script:

1.  **Flask Chatbot Webhook Backend:** A simple webhook service designed to integrate with chatbot platforms (like Dialogflow/API.AI). It handles donation-related intents by identifying a location and suggesting a corresponding (mock) NGO.
2.  **CO₂ Emission Dashboard GUI:** A desktop application built with Tkinter that visualizes historical CO₂ emission data for various countries using data from a CSV file.

---

## Features

### Flask Chatbot Webhook

*   Listens for POST requests on the `/webhook` endpoint.
*   Parses JSON payloads typically sent by chatbot platforms.
*   Identifies specific `action` types (`no.item`, `cloth.don`, `donate.books`).
*   Extracts the `address1` parameter (location).
*   Maps predefined locations (e.g., 'patna', 'buddha colony') to mock NGO names.
*   Returns a JSON response containing a `speech` message indicating which NGO will contact the user.
*   Provides basic request/response logging to the console.

### CO₂ Dashboard GUI

*   Loads CO₂ emission data from `reduced_co2_data.csv`.
*   Allows users to select a specific country from a dropdown list.
*   Allows users to define a start and end year for data filtering.
*   Visualizes data for the selected country and period using various charts:
    *   **Line Chart:** Shows the trend of total CO₂ emissions over the selected years.
    *   **Heatmap:** Displays CO₂ emissions for the selected country across the chosen years (effectively a single-row heatmap).
    *   **Box Plot:** Illustrates the distribution of CO₂ per capita values within the selected period.
    *   *(Note: A "Temperature vs CO₂" chart feature exists in the code but is currently commented out.)*
*   Provides basic textual **Insights:** Calculates and displays average CO₂, average GDP, and the year with the highest CO₂ emission for the filtered data.
*   User-friendly interface built with Tkinter and ttk widgets.
*   Uses Matplotlib and Seaborn for plotting, embedded within the Tkinter window.

---

## Screenshots

*(Add a screenshot of the GUI in action here)*

![Screenshot of CO2 Dashboard GUI](placeholder_screenshot.png) *<-- Replace with an actual screenshot if possible*

---

## Prerequisites

*   Python 3.x
*   pip (Python package installer)
*   The `reduced_co2_data.csv` file present in the same directory as the script. This file should contain columns like `country`, `year`, `co2`, `co2_per_capita`, `gdp`, etc.

---

## Installation & Setup

1.  **Clone the repository (or download the script):**
    ```bash
    git clone <your-repository-url>
    cd <your-repository-directory>
    ```
    Or simply save the provided Python code as a `.py` file (e.g., `app.py`).

2.  **Install required Python libraries:**
    ```bash
    pip install Flask pandas matplotlib seaborn
    ```
    *(Tkinter is usually included with standard Python installations.)*

3.  **Prepare the data file:**
    *   Ensure you have the `reduced_co2_data.csv` file in the same directory as your Python script.

---

## Usage

The script uses a `mode` variable near the end (`if __name__ == '__main__':`) to determine whether to run the Flask server or the Tkinter GUI.

### Running the CO₂ Dashboard GUI

1.  **Set the mode:**
    *   Open the Python script (`app.py` or your chosen name).
    *   Find the line `mode = "flask"` (near the bottom).
    *   Change it to `mode = "gui"`.
2.  **Run the script:**
    ```bash
    python app.py
    ```
3.  **Interact with the GUI:**
    *   Select a country from the dropdown menu.
    *   Enter the desired start and end years.
    *   Click the buttons ("Line Chart", "CO₂ Heatmap", "CO₂ Boxplot", "Get Insight") to view different visualizations or insights based on your selection. The chart area will update accordingly.

### Running the Flask Chatbot Backend

1.  **Set the mode:**
    *   Open the Python script.
    *   Ensure the mode variable is set to `mode = "flask"`.
2.  **Run the script:**
    ```bash
    python app.py
    ```
3.  **Server Status:**
    *   The script will start the Flask development server, typically listening on `http://0.0.0.0:5000` or `http://127.0.0.1:5000`. You'll see output in your terminal indicating it's running.
4.  **Webhook Integration:**
    *   Configure your chatbot platform (e.g., Dialogflow) to use the webhook endpoint.
    *   Set the webhook URL in your chatbot platform to `http://<your-server-ip-or-domain>:5000/webhook`.
    *   If running locally for testing with a cloud platform, you'll likely need a tool like `ngrok` to expose your local port 5000 to the internet. `ngrok http 5000` will provide a public URL you can use.
    *   Ensure your chatbot intents are configured to trigger the actions (`no.item`, `cloth.don`, `donate.books`) and send the `address1` parameter.

---

## Project Structure
