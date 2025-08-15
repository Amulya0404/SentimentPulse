# SentimentPulse Demo Code
# Prototype: AI-Driven Market Mood Analyzer

import random
import time
from textblob import TextBlob
import pandas as pd

# -----------------------------
# Simulated Transaction Data
# -----------------------------
exchanges = ['NYSE', 'NASDAQ', 'BSE', 'CryptoX']
stocks = ['AAPL', 'GOOGL', 'TSLA', 'AMZN', 'BTC', 'ETH']

def generate_transaction():
    return {
        'exchange': random.choice(exchanges),
        'stock': random.choice(stocks),
        'price': round(random.uniform(100, 5000), 2),
        'volume': random.randint(10, 1000),
        'timestamp': pd.Timestamp.now()
    }

# -----------------------------
# Simulated Social Sentiment Data
# -----------------------------
social_comments = [
    "I think AAPL is going to skyrocket!",
    "TSLA is about to crash.",
    "Buy ETH now, huge profits ahead!",
    "GOOGL steady growth expected.",
    "AMZN might be manipulated, suspicious activity."
]

def analyze_sentiment(comment):
    analysis = TextBlob(comment)
    return analysis.sentiment.polarity  # -1 (negative) to +1 (positive)

# -----------------------------
# Detect Abnormal Patterns
# -----------------------------
def detect_anomaly(transaction, sentiment_score):
    # Simple rule-based anomaly detection for demo
    if transaction['volume'] > 800 or sentiment_score < -0.5:
        return True
    return False

# -----------------------------
# Main Demo Loop
# -----------------------------
print("==== SentimentPulse Demo Started ====")
for _ in range(10):  # Simulate 10 transactions
    txn = generate_transaction()
    comment = random.choice(social_comments)
    sentiment = analyze_sentiment(comment)
    anomaly = detect_anomaly(txn, sentiment)
    
    print(f"\nTransaction: {txn}")
    print(f"Related Comment: \"{comment}\"")
    print(f"Sentiment Score: {sentiment:.2f}")
    
    if anomaly:
        print("🚨 ALERT: Suspicious activity detected!")
    else:
        print("✅ Transaction normal.")
    
    time.sleep(1)

print("\n==== Demo Finished ====")
