# Mobile_App_Analysis_Rating_Prediction

## Abstract:

In an era where mobile applications proliferate every aspect of our lives, from entertainment to commerce to daily utilities, understanding what drives app success becomes pivotal. This study dives into an expansive dataset of over 7,000 Apple iOS applications, dissecting the myriad of features and performance metrics that signal market trends and user satisfaction.

Moving beyond mere analysis, the study employs various machine learning models to forecast app success. By leveraging data on app features, such as genre, price, and size, alongside user engagement metrics like rating counts, we aim to predict which factors most significantly influence an app's trajectory in the marketplace. The outcome is a data-driven approach to app evaluation, providing indispensable insights to developers and marketers in the highly competitive app ecosystem.

## Dataset Source Information: 

This project uses the ‘Mobile App Statistics (Apple iOS app store) ’ dataset from Kaggle. 
https://www.kaggle.com/datasets/ramamet4/app-store-apple-data-set-10k-apps

The primary dataset, appleStore.csv, encompasses a comprehensive profile of 7,197 Apple iOS applications, covering an array of 16 distinct attributes. This dataset offers a snapshot of the most current trends within the iOS mobile application landscape. The data compilation was facilitated by harnessing the iTunes Search API, courtesy of Apple Inc. The extraction process was executed using R programming and various Linux-based web scraping tools, ensuring a robust and detailed collection of app-related information for subsequent analysis. The column names and descriptions are as follows:

1.	"id" : App ID  
2.	"track_name": App Name  
3.	"size_bytes": Size (in Bytes)  
4.	"currency": Currency Type  
5.	"price": Price amount  
6.	"rating_count_tot": User Rating counts (for all version)  
7.	"rating_count_ver": User Rating counts (for current version)  
8.	"user_rating" : Average User Rating value (for all version)  
9.	"user_rating_ver": Average User Rating value (for current version) 
10.	"ver" : Latest version code  
11.	"cont_rating": Content Rating  "prime_genre": Primary Genre  
12.	"sup_devices.num": Number of supporting devices  
13.	"ipadSc_urls.num": Number of screenshots shown for display  
14.	"lang.num": Number of supported languages  
15.	"vpp_lic": Vpp Device Based Licensing Enabled 

The appleStore_description.csv dataset contains additional details of textual descriptions of the applications. The column names and descriptions are as follows:

1.	id : App ID 
2.	track_name: Application name 
3.	size_bytes: Memory size (in Bytes) 
4.	app_desc: Application description  

## Analysis Summary:

### 1.	Data Cleaning 

The initial data preparation phase involved importing and inspecting two datasets to identify and rectify missing values. Superfluous variables were excised to streamline the analysis, specifically prioritizing application attributes such as size, price, rating count, content rating, genre, device support, App Store visual elements, language availability, and overall user rating. Data pertaining to obsolete app versions was excluded to maintain a focus on current app features.  

Subsequent transformations refined the dataset further. These included converting measurement units for uniformity, binarizing the 'price' attribute to distinguish free apps, and categorizing variable types. The final step in data preparation involved consolidating the textual app descriptions with the principal dataset, keyed by app IDs, to facilitate a comprehensive analysis.

### 2.	Exploratory Data Analysis

The EDA phase delved into the app market to unearth prevalent trends, characteristics of popular apps, and the dynamics between app features and their ratings—a marker of success. Various visual analytics tools were employed to dissect the genre distribution across free and paid applications, providing insight into user preferences and market saturation.  

A further investigation into the interplay of user ratings with app dimensions such as size and price elucidated potential influences on user satisfaction. Additionally, the role of app genre in the context of user ratings was explored to discern patterns of success across different categories.  

The culmination of the EDA was a correlation study, which highlighted the interdependencies between critical app features. This analysis aimed to identify strong predictors of app success and to understand the nuanced fabric of factors that drive app ratings in the competitive market space.

### 3.	Natural Language Processing 

The NLP stage was pivotal in dissecting the textual content of app descriptions. Initially, this involved the cleansing of text data, which included the removal of numerical digits, punctuation, and ubiquitous stop words that add little semantic value. The refined text was then tokenized, separating paragraphs into individual terms ready for analysis.  

Attention was focused on pinpointing word patterns within the descriptions, highlighting those prevalent in highly rated apps. Visual representations such as frequency plots and word clouds were crafted, offering an intuitive glimpse into the textual trends correlated with user ratings.  

Further deepening the textual analysis, a co-occurrence examination shed light on the symbiotic relationships between words and phrases, revealing the linguistic tapestry that resonates within successful app descriptions.



### 4.	Dimensionality Reduction & Model Selection: 

Before dimensionality reduction, comprehensive feature engineering was executed—applying one-hot encoding to categorical variables and standard scaling to continuous variables—to normalize the data and ensure equitable influence on the model's decisions.
To address the complexity of our multi-featured app data, dimensionality reduction techniques—PCA and t-SNE—were employed. These methods distilled the data into a more manageable form while attempting to retain its most informative aspects. However, the transformation did not result in distinct groupings of high and low-rated apps, suggesting that the feature relationships are complex and not easily separable on a linear scale.  This insight informed our model selection strategy, steering us away from algorithms like KNN and Logistic Regression, which rely on linear separability or proximity in feature space. Instead, we pivoted towards models that can navigate the intricacies of our dataset, such as Decision Trees and Random Forests, which are more adept at handling non-linear patterns and interactions between features. 

### 5.	Decision Tree Classifier Application:  

A Decision Tree Classifier was utilized as the foundational model to predict app ratings, with features consolidated into variable X and a binary high rating outcome (>4) as target Y. The data was partitioned using a 70-30 train-test split. Initially, the model, trained without restrictions, yielded a baseline accuracy of 0.641 via cross-validation—ensuring each prediction was made on data unseen during training, thus providing a robust estimate of performance and mitigating overfitting.  

Cost-complexity pruning refined the model by tuning the ccp_alpha parameter, optimizing for cross-validation accuracy and leading to a more economical model with an improved accuracy of 0.667. This pruned model was then evaluated for its predictive reliability, featuring assessments like a confusion matrix, classification report, and an analysis of feature importance. Cross-validation throughout this process was crucial, as it offered a more reliable accuracy measure by consistently testing the model against unseen data, further safeguarding against overfitting and ensuring the model's generalizability. 

### 6.	Random Forest Classifier Application 

Employing the feature-engineered dataset used for the Decision Tree, a baseline Random Forest model was deployed, leveraging its inherent mechanisms of bagging and feature randomness to mitigate overfitting. The preliminary model, with mostly default settings, delivered an accuracy of 0.685 via cross-validation, indicating a reduction in overfitting compared to the Decision Tree.  

A Random Grid-Search Cross-Validation was executed to optimize the model, focusing on key hyperparameters such as the number of estimators and tree depth, to strike a balance between model complexity and computational efficiency. With its ideal parameters, the resulting refined Random Forest model slightly improved the accuracy to 0.686. 

Further enhancement involved integrating textual data processed through a TFIDF vectorizer, fine-tuned to account for the most relevant terms (max_features) and term frequency (max_df). The augmented dataset underwent a new train-test split, followed by another round of Random Grid-Search to fine-tune the model parameters. This comprehensive model, encapsulating both textual and traditional features, advanced the accuracy to 0.693, showcasing the value of text analytics in predictive modeling.  

The model's performance was substantiated through various metrics, including a confusion matrix, classification report, and feature importance analysis, ensuring a holistic evaluation of its predictive prowess.








