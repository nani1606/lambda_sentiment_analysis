# lambda_sentiment_analysis
# IPL 2025 Tweet Sentiment Analysis Pipeline

A cloud-based data pipeline to fetch, process, store, and visualize real-time IPL tweet sentiment using AWS, Python, and Tableau. Built to demonstrate Cloud Data Engineering skills for database management, cloud services, and data pipelines.

## Overview
This project analyzes sentiment of tweets from IPL 2025 (Gujarat Titans vs. Rajasthan Royals, Match 23). It:
- Fetches tweets via the X API.
- Computes sentiment scores using TextBlob.
- Stores raw data in AWS S3 and structured data in AWS RDS (MySQL).
- Processes real-time tweets with AWS Lambda.
- Visualizes results in a Tableau dashboard.

# IPL 2025 Tweet Sentiment Analysis Pipeline

A cloud-based data pipeline to fetch, process, store, and visualize real-time IPL tweet sentiment using AWS, Python, and Tableau. Built to demonstrate Cloud Data Engineering skills for database management, cloud services, and data pipelines.

## Overview
This project processes tweets related to IPL 2025 (Gujarat Titans vs. Rajasthan Royals) to analyze fan sentiment. It:
- Fetches tweets via the X API.
- Computes sentiment scores using TextBlob.
- Stores raw data in AWS S3 and structured data in AWS RDS (MySQL).
- Processes real-time tweets with AWS Lambda.
- Visualizes results in a Tableau dashboard.

The pipeline flows as follows:
- **X API**: Streams IPL tweets.
- **Python (Local)**: Initial fetch and sentiment analysis (50 tweets).
- **AWS S3**: Stores raw CSV and processed JSONs.
- **AWS Lambda**: Automates real-time tweet processing (10 tweets per run).
- **AWS RDS (MySQL)**: Stores structured tweet data (text, sentiment).
- **Tableau Public**: Visualizes average sentiment and tweet count.

## Setup
### Prerequisites
- AWS account (free tier)
- X API access (Bearer Token)
- Tableau Public account
- Python 3.12 with libraries: `tweepy`, `textblob`, `boto3`, `mysql-connector-python`

### Steps
1. **Fetch Tweets**:
   - Run `fetch_tweets.py` cell to collect 50 IPL tweets and save to `ipl_tweets.csv`.
2. **Store in S3**:
   - Run `upload_s3.py` to upload CSV to `krishna-ipl-tweets` bucket.
3. **Load to RDS**:
   - Run `load_rds.py` to populate MySQL table (`tweets`) in `ipl_db`.
4. **Automate with Lambda**:
   - Deploy `lambda_function.py` with dependencies (`tweepy`, `textblob`, `boto3`) as `lambda_ipl.zip`.
   - Processes 10 tweets per invocation, saves JSONs to S3.
5. **Visualize**:
   - Import `ipl_tweets.csv` (or export from RDS) into Tableau Public.
   - Create dashboard with average sentiment and tweet count.

## Results
- **Data**: Processed 50 tweets from GT vs. RR (Match 23, IPL 2025).
- **Sentiment**: Average sentiment ~0.2 (slightly positive, reflecting GT’s win).
- **Tweet Count**: 50 tweets analyzed (local), 10+ per Lambda run.
- **Dashboard**: Visualized in Tableau: [IPL Sentiment Dashboard](https://public.tableau.com/views/practice_17443145966300/Sheet1)
- **Sample Insight**: Positive sentiment spikes for Sai Sudharsan’s 82-run knock.

## Challenges
- **Lambda Dependencies**: Initial `No module named 'tweepy'` error resolved using `--platform manylinux2014_x86_64` for Linux-compatible packages.
- **X API Limits**: Rate limits restricted real-time streaming; mitigated by batch fetching.
- **RDS Setup**: Ensuring public accessibility and security group rules (port 3306) required careful configuration.

## Future Improvements
- Automate RDS updates from Lambda.
- Add more visuals (e.g., sentiment trends over time).
- Integrate advanced NLP (e.g., VaderSentiment for better accuracy).

## Architecture
```mermaid
graph TD
    A[X API<br>Tweets] --> B[Python Local<br>fetch_tweets.py]
    B --> C[AWS S3<br>ipl_tweets.csv]
    B --> D[AWS RDS<br>ipt_db.tweets]
    A --> E[AWS Lambda<br>iptTweetProcessor]
    E --> F[AWS S3<br>processed_tweets/]
    D --> G[Tableau Public<br>Dashboard]
