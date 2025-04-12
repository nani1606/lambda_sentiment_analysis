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

## Architecture
```mermaid
graph TD
    A[X API<br>Tweets] --> B[Python Local<br>fetch_tweets.py]
    B --> C[AWS S3<br>ipl_tweets.csv]
    B --> D[AWS RDS<br>ipt_db.tweets]
    A --> E[AWS Lambda<br>iptTweetProcessor]
    E --> F[AWS S3<br>processed_tweets/]
    D --> G[Tableau Public<br>Dashboard]
