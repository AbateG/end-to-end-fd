import requests
import pandas as pd
import psycopg2
from io import StringIO
import logging
import os 
from dotenv import load_dotenv 


load_dotenv()


STOCKS_TO_PROCESS = ['MSFT', 'AAPL', 'GOOG', 'AMZN'] 


DB_NAME = 'financial_data'
DB_USER = 'postgres'
DB_PASSWORD = os.getenv('DB_PASSWORD')
DB_HOST = 'localhost'
DB_PORT = '5432'
API_KEY = os.getenv('API_KEY')


logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler("pipeline.log"), 
        logging.StreamHandler() 
    ]
)

def get_db_connection():
    """Establishes and returns a database connection."""
    conn = psycopg2.connect(
        dbname=DB_NAME, user=DB_USER, password=DB_PASSWORD, host=DB_HOST, port=DB_PORT
    )
    return conn

def run_pipeline():
    """Runs the full ETL pipeline for all configured stocks."""
    logging.info("Starting financial data pipeline...")
    
    for symbol in STOCKS_TO_PROCESS:
        logging.info(f"--- Processing symbol: {symbol} ---")
        
        try:
            logging.info(f"Step 1: Extracting data for {symbol}.")
            url = f'https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol={symbol}&apikey={API_KEY}&outputsize=full'
            response = requests.get(url)
            response.raise_for_status()
            data = response.json()
            
            if 'Time Series (Daily)' not in data:
                logging.warning(f"Could not find time series data for {symbol}. API response: {data}")
                continue 

            logging.info(f"Step 2: Transforming data for {symbol}.")
            time_series_data = data['Time Series (Daily)']
            df = pd.DataFrame.from_dict(time_series_data, orient='index')
            
            df.rename(columns={
                '1. open': 'open', '2. high': 'high', '3. low': 'low', 
                '4. close': 'close', '5. volume': 'volume'
            }, inplace=True)
            
            df.reset_index(inplace=True)
            df.rename(columns={'index': 'date'}, inplace=True)
            df['symbol'] = symbol
            
            logging.info(f"Step 3: Loading data for {symbol} into PostgreSQL.")
            conn = get_db_connection()
            cursor = conn.cursor()

            buffer = StringIO()
            df.to_csv(buffer, index=False, header=False)
            buffer.seek(0)
            
            cursor.copy_expert(
                sql="COPY daily_prices(date, open, high, low, close, volume, symbol) FROM STDIN WITH (FORMAT CSV)",
                file=buffer
            )
            conn.commit()
            
            cursor.close()
            conn.close()
            
            logging.info(f"Successfully loaded {len(df)} rows for {symbol}.")

        except requests.exceptions.RequestException as e:
            logging.error(f"HTTP Request failed for {symbol}: {e}")
        except psycopg2.Error as e:

            if "duplicate key value violates unique constraint" in str(e).lower():
                logging.warning(f"Data for {symbol} likely already exists. Skipping.")
                conn.rollback()
            else:
                logging.error(f"Database error for {symbol}: {e}")
        except Exception as e:
            logging.error(f"An unexpected error occurred for {symbol}: {e}")

    logging.info("Financial data pipeline finished successfully.")

if __name__ == '__main__':
    run_pipeline()