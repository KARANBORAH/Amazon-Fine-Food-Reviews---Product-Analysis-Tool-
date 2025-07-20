# Amazon-Fine-Food-Reviews---Product-Analysis-Tool-
A comprehensive Python tool for analyzing Amazon Fine Food product reviews to extract insights, sentiment patterns, and customer feedback trends.
🎯 Overview
This project provides an in-depth analysis of Amazon Fine Food Reviews dataset, focusing on understanding customer sentiment, product performance, and review patterns. Unlike machine learning models, this tool emphasizes exploratory data analysis and actionable business insights.
📋 Features
Core Analysis Capabilities

Product Discovery: Identify top-reviewed and highest-rated products
Sentiment Analysis: Understand customer emotions using TextBlob
Keyword Extraction: Find common themes in positive/negative reviews
Trend Analysis: Track rating changes over time
Comparative Analysis: Compare multiple products side-by-side
Visual Dashboards: Interactive charts and word clouds

Key Metrics Analyzed

⭐ Average ratings and distribution
📊 Review volume and frequency
💭 Sentiment polarity (Positive/Negative/Neutral)
🔑 Most common keywords by sentiment
📅 Review trends over time
📝 Review length patterns

🛠️ Installation
Prerequisites
bashpip install pandas numpy matplotlib seaborn textblob wordcloud
Additional Setup
python# Download required NLTK data (run once)
import nltk
nltk.download('punkt')
nltk.download('vader_lexicon')
📂 Dataset
Source: Amazon Fine Food Reviews on Kaggle
Dataset Info:

568,454 food product reviews
256,059 unique products
74,258 users
Time span: Oct 1999 - Oct 2012
Review scores: 1-5 stars

Key Columns:

ProductId: Unique product identifier
Score: Rating (1-5 stars)
Text: Review content
Summary: Review title
Time: Unix timestamp
UserId: User identifier

🚀 Quick Start
1. Basic Setup
pythonimport pandas as pd
from product_review_analyzer import *  # Import all functions

# Load dataset
df = pd.read_csv('/kaggle/input/amazon-fine-food-reviews/Reviews.csv')
2. Run Complete Analysis
python# The script automatically analyzes the most reviewed product
# Just run the main script to get comprehensive insights
3. Analyze Specific Product
python# Deep dive into any product
product_data = analyze_product_reviews('B001E4KFG0', df)

# Create visualizations
create_product_visualizations(product_data, 'B001E4KFG0')
4. Quick Product Overview
python# Fast analysis of any product
result = quick_product_analysis('B001E4KFG0')
print(result)
5. Compare Products
python# Compare multiple products
products_to_compare = ['B001E4KFG0', 'B00813GRG4', 'B000LQOCH0']
comparison = compare_products(products_to_compare, df)
📊 Sample Output
🔍 DETAILED ANALYSIS: Product B001E4KFG0
============================================================
Total Reviews: 1,324
Average Rating: 4.74/5
Rating Std Dev: 0.85

⭐ RATING BREAKDOWN:
1⭐:  23 reviews ( 1.7%)
2⭐:  25 reviews ( 1.9%)
3⭐:  37 reviews ( 2.8%)
4⭐: 202 reviews (15.3%)
5⭐: 1037 reviews (78.3%)

💭 SENTIMENT ANALYSIS:
Positive: 87 (87.0%)
Neutral: 8 (8.0%)
Negative: 5 (5.0%)

🔑 COMMON KEYWORDS:
Positive Reviews Keywords: ['delicious', 'great', 'love', 'perfect', 'amazing']
Negative Reviews Keywords: ['expensive', 'small', 'disappointed', 'bland', 'poor']
📈 Key Functions
analyze_product_reviews(product_id, df)
Comprehensive analysis including:

Rating distribution and statistics
Sentiment analysis of reviews
Keyword extraction for positive/negative reviews
Time-based trends
Sample best/worst reviews

compare_products(product_ids, df)
Side-by-side comparison showing:

Total reviews count
Average ratings
Sentiment percentages
Recent review activity

create_product_visualizations(product_data, product_id)
Generates 4 visualization panels:

Rating distribution bar chart
Rating trends over time
Review length vs rating scatter plot
Word cloud of common terms

quick_product_analysis(product_id)
Fast overview providing:

Basic statistics
Sentiment distribution
Latest review date

📋 Use Cases
For E-commerce Managers

Product Performance: Identify top and bottom performers
Customer Satisfaction: Monitor sentiment trends
Quality Issues: Spot products with declining ratings
Competitive Analysis: Compare similar products

For Marketing Teams

Customer Voice: Understand what customers love/hate
Feature Highlighting: Extract positive keywords for marketing
Problem Areas: Identify common complaints
Seasonal Trends: Track review patterns over time

For Product Developers

Improvement Areas: Analyze negative feedback themes
Success Factors: Understand what makes products successful
User Experience: Review length and sentiment patterns
Feature Requests: Extract customer suggestions

🔧 Customization
Modify Sentiment Thresholds
pythondef analyze_sentiment(text):
    blob = TextBlob(str(text))
    polarity = blob.sentiment.polarity
    
    # Customize these thresholds
    if polarity > 0.2:  # More strict positive
        sentiment = 'Positive'
    elif polarity < -0.2:  # More strict negative
        sentiment = 'Negative'
    else:
        sentiment = 'Neutral'
    
    return sentiment, polarity, blob.sentiment.subjectivity
Add Custom Keywords
python# Extend stop words list
custom_stop_words = {'food', 'product', 'item', 'amazon', 'buy', 'purchase'}
# Add to existing stop_words set in extract_keywords function
Filter by Date Range
python# Analyze recent reviews only
recent_df = df[pd.to_datetime(df['Time'], unit='s') > '2010-01-01']
analyze_product_reviews('B001E4KFG0', recent_df)
📊 Performance Considerations

Large Dataset: Script processes 500K+ reviews efficiently
Sampling: Uses intelligent sampling for sentiment analysis (first 100 reviews per product)
Memory Usage: Optimized for Kaggle environment (16GB RAM)
Processing Time: Full analysis takes 2-5 minutes depending on product size

For Better Performance
python# Analyze smaller subset
df_sample = df.sample(n=50000, random_state=42)

# Focus on recent reviews only
df_recent = df[df['Time'] > df['Time'].quantile(0.8)]
📈 Advanced Analysis Ideas
Seasonal Patterns
pythondf['Month'] = pd.to_datetime(df['Time'], unit='s').dt.month
seasonal_sentiment = df.groupby('Month')['Score'].mean()
User Behavior Analysis
pythonuser_stats = df.groupby('UserId').agg({
    'Score': ['mean', 'count', 'std'],
    'Text': lambda x: x.str.len().mean()
})
Product Category Insights
python# If you have category data
category_performance = df.groupby('Category').agg({
    'Score': 'mean',
    'ProductId': 'nunique',
    'Text': 'count'
})
🐛 Troubleshooting
Common Issues
Issue: KeyError: 'ProductId'
Solution: Ensure dataset is loaded correctly with all required columns
Issue: Memory errors with large datasets
Solution: Use sampling or filter by date range
Issue: Empty results for product analysis
Solution: Check if ProductId exists using df['ProductId'].unique()
Debug Commands
python# Check available products
print(f"Available products: {df['ProductId'].nunique()}")
print(f"Most reviewed products: {df['ProductId'].value_counts().head()}")

# Verify data integrity
print(f"Missing values: {df.isnull().sum()}")
print(f"Date range: {pd.to_datetime(df['Time'], unit='s').min()} to {pd.to_datetime(df['Time'], unit='s').max()}")
📝 Example Workflow
python# 1. Load and explore data
df = pd.read_csv('/kaggle/input/amazon-fine-food-reviews/Reviews.csv')
print(f"Dataset shape: {df.shape}")

# 2. Find interesting products
top_products = df['ProductId'].value_counts().head(10)
print("Top 10 products by review count:", top_products)

# 3. Analyze specific product
target_product = top_products.index[0]  # Most reviewed product
product_analysis = analyze_product_reviews(target_product, df)

# 4. Create visualizations
create_product_visualizations(product_analysis, target_product)

# 5. Compare with competitors
similar_products = top_products.index[1:4]  # Next 3 products
comparison = compare_products([target_product] + similar_products.tolist(), df)

# 6. Generate insights
print("\n📋 KEY INSIGHTS:")
print(f"- Product {target_product} has {len(product_analysis)} reviews")
print(f"- Average sentiment is predominantly positive")
print(f"- Main complaint themes: [extracted from analysis]")
print(f"- Recommendation: [based on findings]")
🤝 Contributing
Feel free to enhance this analysis tool by:

Adding new visualization types
Implementing advanced NLP techniques
Creating export functionality for reports
Adding statistical significance tests
Implementing product recommendation features

📄 License
This project is open source and available under the MIT License.
🙏 Acknowledgments

Amazon and Stanford SNAP for providing the dataset
TextBlob library for sentiment analysis
Kaggle platform for hosting and compute resources
Python data science community for excellent libraries


Happy Analyzing! 📊✨
For questions or improvements, feel free to reach out or create an issue.
