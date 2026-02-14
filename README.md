# codealpha_tasks
## Netflix Content Analysis (EDA Project)
### Overview
This project analyzes Netflix’s content library to understand content growth, strategy, and trends over time.

Using Python and Exploratory Data Analysis (EDA), the dataset was explored to understand how Netflix has evolved its focus across Movies, TV Shows, countries, and duration patterns.

The main objective of this project is to extract meaningful business insights from raw data and present them in a clear and structured manner.

### Dataset Information
- Dataset Name: Netflix Titles Dataset
- Source: Public Netflix dataset (CSV format)
- Records: Movies and TV Shows available on Netflix

### Key Columns
- Type (Movie / TV Show)
- Title
- Country
- Director
- Cast
- Date Added
- Release Year
- Rating
- Duration
- Genre (listed_in)

### Business Questions Before Analysis
Before starting the analysis, the following questions were defined:
- How has Netflix’s content grown over the years?
- Does Netflix focus more on Movies or TV Shows?
- Which countries contribute the most content?
- Is Netflix shifting toward long-term engagement content?
- What data quality issues exist in the dataset?

### Data Cleaning and Preparation
The dataset contained missing and inconsistent values. The following steps were performed:
- Identified missing values using isnull()
- Replaced missing values using fillna()
- Converted date columns into datetime format
- Extracted year_added from date_added
- Standardized duration into numeric format
- Created duration type (Minute / Season)
- Created country count feature for multi-country titles

## Commands and Methods Used
### 1. Understanding the Data
Used to explore structure and summary:
- df.head()
- df.tail()
- df.shape
- df.columns
- df.info()
- df.describe()

### 2. Handling Missing Values
- df.isnull().sum()
- df['country'] = df['country'].fillna("Unknown")
- df['rating'] = df['rating'].fillna("No Rating")
- df['date_added'] = pd.to_datetime(df['date_added'], errors='coerce')

### 3. Feature Engineering
Extract year from date:
- df['year_added'] = df['date_added'].dt.year

Convert duration into numeric:
- df['duration_num'] = df['duration'].str.extract('(\d+)').astype(float)

Classify duration type:
- df['duration_type'] = df['duration'].apply(
    lambda x: 'Season' if 'Season' in str(x) else 'Minute'
)

Count number of countries per title:
- df['country_count'] = df['country'].apply(
    lambda x: len(str(x).split(','))
)

### 4. Trend and Pattern Analysis
Used grouping and frequency functions:
- df['type'].value_counts()
- df.groupby('type')['duration_num'].mean()
- df.groupby('year_added')['type'].count()
- df.sort_values(by='year_added')

## Exploratory Data Analysis (EDA)
### Content Growth Over Time
- Netflix content increased rapidly in earlier years.
- Growth has slowed recently, indicating a shift toward content quality.

### Movies vs TV Shows
- Movies dominate in overall count.
- TV Shows are increasing steadily, supporting long-term user retention.

### Country Analysis
- Netflix has expanded beyond the United States.
- International content plays a major role in platform growth.

### Duration Insights
- Movies generally have shorter durations.
- TV Shows span multiple seasons, encouraging long-term engagement.

## Data Visualization
Data Visualization was used to represent findings clearly using charts and graphs.

### Visualization Tools Used
- Python
- Jupyter Notebook
- Matplotlib
- Seaborn

### Visualization Commands
import matplotlib.pyplot as plt
import seaborn as sns
plt.style.use('ggplot')

### Types of Visualizations Created
- Movies vs TV Shows comparison
- Year-wise content addition
- Genre distribution
- Rating distribution
- Duration distribution
- Correlation heatmap

Example:
sns.countplot(x='type', data=df)

## Key Business Insights
- Netflix has shifted from rapid expansion to engagement-driven strategy.
- TV Shows are critical for long-term subscriber retention.
- International markets significantly contribute to growth.
- Content decisions appear strategic rather than volume-focused.

## Limitations of the Analysis
- No user engagement data (watch time, views, ratings).
- No performance metrics for individual titles.
- Country column contains multiple values in single cells.
- Duration formats are partially inconsistent.

These limitations restrict deeper behavioral and predictive analysis.

## Future Scope
If additional data were available, future work could include:
- User engagement and watch-time analysis
- Rating-based performance analysis
- Regional content preference study
- Content success prediction models

## Exporting Cleaned Data
The cleaned dataset was exported for reporting purposes:
df.to_csv("netflix_updated.csv", index=False)
df.to_excel("netflix_updated.xlsx", index=False)

## Tools and Technologies Used
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## Conclusion
This project demonstrates the ability to:
- Define structured business questions
- Clean and prepare real-world datasets
- Perform systematic exploratory data analysis
- Create meaningful visualizations
- Communicate insights in a clear and professional manner

The analysis indicates that Netflix focuses on strategic content growth, international expansion, and long-term user engagement rather than simply increasing content volume.
