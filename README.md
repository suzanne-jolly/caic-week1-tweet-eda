# caic-week1-tweet-eda
CAIC Summer of Tech 2025 – Week 1 Submission

Project: Predicting Tweet Likes + Generating Tweet Text from Metadata  


# Dataset
We worked with a dataset of ~17,000 tweets. Each record includes:
- Tweet metadata (username, date, media, etc.)
- Tweet text (`content`)
- Engagement (`likes`)

---

# Data Cleaning Steps
- Dropped rows with missing `content`, `username`, `company`, or `likes`
- Filled missing media with `"no_media"`
- Created boolean flag `has_media`
- Converted `date` column to `datetime`
- Standardized tweet text: lowercase, stripped whitespace

---

# Exploratory Data Analysis (EDA)

### 1. Likes Distribution
- Most tweets have low to moderate likes
- A small number of tweets go viral (outliers)


### 2. Tweet Timing
- Extracted `hour` and `day_of_week` from `datetime`
- Most tweets are posted in the afternoon
- Weekdays dominate tweet activity

### 3. Text Features
- Added `word_count` and `char_count` features
- Most tweets are short (~10–15 words)

### 4. Media Usage
- Binary `has_media` flag created
- Tweets with media may drive more engagement

### 5. Brand Distribution
- Top companies with the most tweets were visualized
- Brands like Nike, Apple, and Netflix are highly active

### 6.  Username Distribution (Optional Insight)
- Some usernames appear much more frequently, indicating brand official accounts or highly active users.
- This skew suggests uneven tweet activity across users.
---

##  Final Feature List for Modeling

| Feature         | Description                                            |
|----------------|--------------------------------------------------------|
| `username`      | Account that posted the tweet                         |
| `inferred company` | Brand or company associated with the tweet       |
| `has_media`     | Boolean flag indicating if tweet contains media       |
| `hour`          | Hour of the day the tweet was posted (0–23)           |
| `day_of_week`   | Day of the week the tweet was posted (e.g., Monday)   |
| `word_count`    | Number of words in the tweet's content                |
| `char_count`    | Number of characters in the tweet's content           |

> Target variable: `likes`

---

##  API Structure Plan

###  Sample Input (from Frontend):
```json
{
  "username": "apple",
  "company": "Apple",
  "content": "Introducing our most powerful MacBook yet",
  "media": "image",
  "datetime": "2025-07-07 14:30:00"
}

```

### Backend feature engineering includes deriving the following attributes: 
- `has_media`: computed from media, 
- `word_count`: extracted from content, 
- `char_count`: derived from content, 
- `hour` and `day_of_week`: extracted from datetime.

Sample output to the frontend:

```json

{
  "predicted_likes": 850
}
```
