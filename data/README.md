Due to GitHub's file size limit (100 MB), the raw `zomato.csv` file (~120 MB) is not tracked directly in this repository. This directory contains the necessary documentation to download, place, and map the source dataset to run the analytical pipelines successfully.

## 📥 Source & Dataset Details

- **Database Source:** Kaggle — Zomato Bangalore Restaurants
- **Dataset Size:** ~120 MB (Uncompressed CSV)
- **Volume:** 51,717 rows × 17 columns (Raw)
- **Format:** Comma Separated Values (.csv)

## ⚙️ How to Set Up the Data

To run the Jupyter Notebook in this repository, follow these quick setup instructions based on your environment:

### Method A: Running on Google Colab (Recommended)

1. Download the raw `zomato.csv` from the Kaggle link above.
2. Upload the file to your Google Drive under this exact directory path:
`My Drive/Zomato_Project/zomato.csv`
3. Open the notebook in Google Colab and execute the mounting cells. The pipeline will automatically stream the data securely from your Drive.

### Method B: Running Locally (Jupyter / VS Code)

1. Clone this repository to your machine.
2. Download the raw `zomato.csv` from Kaggle.
3. Move the downloaded `zomato.csv` file directly into this `/data/` folder.
4. Open `notebooks/zomato_bangalore_market_analysis.ipynb` and change the loading path in Phase 1 to:
    
    ```
    df = pd.read_csv('../data/zomato.csv')
    ```
    

## 🗺️ Raw Schema Dictionary (Before Preprocessing)

Here is a map of the original raw variables before we executed our Phase 3 data cleaning pipeline:

| Column Name | Data Type | Description | Handling in our Pipeline |
| --- | --- | --- | --- |
| `url` | Object | Zomato URL for the restaurant | **Dropped** (Administrative noise) |
| `address` | Object | Full street address of the restaurant | **Dropped** (Housed in clean city column) |
| `name` | Object | Name of the restaurant | **Standardized** to clean Title Case |
| `online_order` | Object | Offers online ordering (Yes/No) | **Kept** (Used for service feature analysis) |
| `book_table` | Object | Allows table booking (Yes/No) | **Kept** (Used for service feature analysis) |
| `rate` | Object | Customer rating (e.g., `'4.1/5'`, `'NEW'`, `'-'`) | **Cleaned & Normalized** to floating decimals |
| `votes` | Integer | Total count of user ratings submitted | **Kept** (Used to measure engagement) |
| `phone` | Object | Contact number of the business | **Dropped** (No statistical value) |
| `location` | Object | General neighborhood area | **Kept** (Used for micro-location analysis) |
| `rest_type` | Object | Type of restaurant (e.g., Cafe, Casual) | **Renamed** to `type` & Standardized |
| `dish_liked` | Object | Dishes most liked by customers | **Dropped** (High null volume > 54%) |
| `cuisines` | Object | Cuisines offered (comma-separated list) | **Standardized** (Used for demand analysis) |
| `approx_cost(...)` | Object | Estimated cost of a meal for two people | **Cleaned, cast to Float, & Renamed** to `cost` |
| `reviews_list` | Object | Raw text reviews list with scores | **Dropped** (High-memory text blocks) |
| `menu_item` | Object | Menu items available at the restaurant | **Dropped** (Large volume of empty lists `[]`) |
| `listed_in(type)` | Object | Category of dining (e.g., Delivery, Dine-out) | **Renamed** to `category` |
| `listed_in(city)` | Object | Broad neighborhood sector | **Renamed** to `city` & Standardized |
