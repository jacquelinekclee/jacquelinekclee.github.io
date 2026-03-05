---
layout: page
title: 🎵⏪ Play Back - Music Streaming History Deep Dive
description: Description of music streaming history analysis app, Play Back 
nav_order: 4
---

<p style = "float: left"> 
    <h1 style = "float: left">🎵⏪ Play Back - Music Streaming History Deep Dive</h1>
</p>

# Summary 

As a loyal user of music streaming service of Tidal since 2020, the FOMO with Spotify Wrapped was real at the end of each year. While most music streaming services today have their own version of Spotify Wrapped, users still have to wait a full year to get a peek into their listening habits. As an avid music listener, who leverages both streaming services and my personal music library, and self-proclaimed Data Nerd, I wanted to build something that allows folks, no matter which streaming service they use, to understand their music listening habits. 

With Play Back, you can explore your streaming history with interactive charts and graphs, from high-level streaming patterns to detailed yearly and quarterly heatmaps. Take your analysis to the next level by using Machine Learning to uncover your unique listening session types. There's options for uploading your own last.fm data for a personalized experience, or you can explore the app with my own *real* music streaming data. 

Check out Play Back on Streamlit linked [here](share_link) and [below](links). 

There's also an option to run the data processing and model building pipelines if you'd like to process your raw data from last.fm for your own analysis. 

For running locally, see the [instructions below](#run-play-back-locally). 

# 👩🏻‍💻 Skills Used
- Data cleaning and processing 
- Data visualization
- Machine learning - hyperparameter tuning, model training, and interpretation of output
- Web app building

# ⚙️ Technologies Used
- `scikit-learn` for building and training a machine learning model (k-means clustering) 
- `Python` (including `Pandas` and `NumPy`) data cleaning, processing, and feature engineering  
- `Streamlit` for building the web app user interface
- `Claude` for Gen AI-assisted ideation and building
- `bash` for configuring the data processing and model building pipeline to give users a command-line experience  

# Links
[![Try it in Streamlit][share_badge]][share_link] 
- [Repository (with all code and other files)](https://github.com/jacquelinekclee/lastfm_analysis)

# On this page

- [Run Play Back Locally](#run-play-back-locally)
- [Listening Session Clustering Model](#listening-session-clustering-model)

# Run Play Back Locally

## Run the Streamlit App Locally

### Installation & Environment Setup

1. Clone the repository:
```bash
   git clone https://github.com/jacquelinekclee/lastfm_analysis.git
   cd lastfm_analysis
```

2. Create a virtual environment (recommended):
```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
   pip install -r requirements.txt
```

### Run the App
```bash
   streamlit run 0_🎵⏪_Play_Back_Home_Page.py
```

The Streamlit app will open in your browser at `http://localhost:8501`

## Run the Scripts Only
If you'd like to process your own streaming data and/or run the listening sessions clustering model, without running the full streamlit app, you can do so via the command line and the scripts in this repo. 

### Setup
First, follow the same [installation and setup](#installation--environment-setup) instructions above. 

#### Download Your Raw Streaming Data
Leverage a [website like this one](https://mainstream.ghan.nl/export.html]) to download your raw streaming data from last.fm.

Then, **move this file** (should be .csv) into the `data/raw` directory. 

#### Configurate Parameters
**Update `scrobbles_fp` in the `config/data_params.json` file** to a filename of your choice. This is essential!
Feel free to play around with any the configurations in `config/data_params.json`. 

### Run the Streaming Data Processing and K-Means Clustering of your Listening Sessions

#### Run Both Workstreams
After [downloading your raw streaming data from last.fm](#download-your-raw-streaming-data) as described above, you can run both the data processing and k-means clustering model workstreams with the following script:
```bash
python3 run.py {n_clusters}
```
Where `n_clusters` is an optional parameter that defines how many clusters you want your k-means model to identify. If this is omitted, the default value is 4. `n_clusters` must be an integer of at least 2, and I recommend no greater than 6. 

#### Run the Data Processing Workstream
To run just the data processing workstream:
```bash
python3 process_data.py
```

#### Run the K-Means Clustering Workstream
To run just the listening sessions clustering model, you must have already processed your raw streaming data using the script above and ensure that `processed_scrobbles_fp` in `config/data_params.json` is updated and your processed streaming data csv file is in the `data/processed` directory:
```bash
python3 perform_clustering.py {n_clusters}
```
Where `n_clusters` is an optional parameter that defines how many clusters you want your k-means model to identify. 

#### Run Scripts with Test Data
To test any of the scripts, simply include `test` as shown below. `test` must be the first argument provided. 
```bash
python3 run.py test {n_clusters}
```

[(Back to top)](#summary)

# Listening Session Clustering Model
## Background
I wanted to uncover whether there are any trends in my listening habits in order to more deeply understand not only *what* I listen to, but *how* I listen to that music. To do so, I:
1. Extracted "listening sessions" from my raw streaming data tracked by last.fm. A listening session is defined by consecutive streams of songs with no less than 10 minutes in between each stream to account for long songs and brief interruptions. 
2. Trained a k-means clustering model so machine learning can identify my typical listening patterns. 

After processing the data, extracting listening sessions, calculating listening session metrics, like proportion of unique artists, albums, and songs listened to, and scaling these features, I was ready to train my clustering models. 

## Model Training
Since my original listening session data had 10+ features detailing session length, date and time, and diversity of music, many of which were highly correlated, I knew I had to implement some sort of feature selection/dimensionality reduction technique. I looked into 2 options:
1. Reviewing multicollinearity with a correlation matrix and selecting features that aren't highly correlated with one another
2. Leveraging principal component analysis to calculate 2-3 condensed features that capture all the variance in my listening sessions data. 

For both options, I leveraged the elbow method to land on an optimal `k`, or number of clusters. Based on this method, `k=4` was the optimal choice across both techniques described abov. 

## Model Selection
I analyzed cardinality, centroid distances, and magnitude (sum of distances of each point/session from its cluster centroid), the model that leveraged simple feature filtering proved to be best. Cardinality and average centroid distances were relatively uniform across al 4 clusters and cardinality vs. magnitude saw the stronger positive correlation (ideal since the greater the number of examples in a cluster, the greater we expect the total distance to be). 

## Clustering Output Analysis 
After reviewing inter- and intra-cluster distributions for the various features of each listening session (e.g., time of day, diversity of music, and whether any first listens occured), I identified the key characteristics of each cluster. With the help of Claude, I defined my listening session clusters:
1. Weekend wind down: sessions typically on the weekends that consist of my go-to songs and favorite artists. 
2. New discovery: sessions where I catch up singles released on new music Friday or listen to an album in full for the first time soon after its release. 
3. Deep dive marathon: sessions during which I'm listening to some sort of playlist or assortment of songs. I predict these are from long commutes or gym sessions.
4. Late night faves: quick listening sessions during late nights or the wee hours of the morning where I'm jamming to my old reliables. 

See listening session examples of each of these clusters in [Play Back on Streamlit][share_link], and then build your own clustering model to uncover similar insights! 


[(Back to top)](#summary)

[share_badge]: https://static.streamlit.io/badges/streamlit_badge_black_white.svg
[share_link]: https://playback-analytics.streamlit.app/
