# End-to-End Financial Data Pipeline

## 📖 Description

The project elaborates on an end-to-end data pipeline that extracts, in a daily automatic manner, the data from the stock market for multiple tickers, processes it, and loads it into a PostgreSQL database. Docker containerises the entire application to ensure its portability and consistency.

---

## ✨ Features

🔸Firstly, it extracts data from the Alpha Vantage API with the intention to transform it with Pandas and then load it into PostgreSQL. 

🔸Secondly, it is easily configurable to process a list of multiple stock tickers.

🔸Thirdly, it has robust logging due to the fact that it creates a pipeline and log file to track all the corresponding operations and errors with the objective to monitor them easily.

🔸Fourth, it uses environment variables to securely store API keys and database passwords outside of the codebase.

🔸Fifth, it is fully containerised with Docker and Docker Compose with the intention to have a consistent and isolated environment.

🔸Sixth, it is scheduled, meaning that it is designed to be run in an automatic manner on a daily basis by employing Windows Task Scheduler or cron.

---

## 🛠️ Tech Stack

🔸 **Language:** Python

🔸 **Libraries:** Pandas, Requests, psycopg2, python-dotenv

🔸 **Database:** PostgreSQL

🔸**Containerization:** Docker & Docker Compose

---

## 🚀 How to Run

To run it, you need to:

🔸 Clone this repository to your local machine.

🔸 Ensure you have Docker Desktop installed and running.

🔸 Create a .env file in the root directory and add your credentials:
DB_PASSWORD="your_db_password" API_KEY="your_api_key"

🔸 From the project's root directory, run the required Docker command (**Docker compose**) in the corresponding portal to build the necessary images and start the pipeline. 

---

## 📸 Screenshots

*(Here, you can add screenshots of your running application, the log file, or the data in the database!)*