# 🚘 Traffic Collision Severity Prediction 🚘

## 🌍 Overview
Traffic collisions are increasingly becoming more common and are already a leading cause of death. While there have been other studies on this topic, most use post-collision factors, so the proactive prediction of collision severity remains relatively unexplored. This project aims to fill this gap by developing a machine learning model capable of predicting the severity of a traffic collision using only pre-collision variables.

**I also wrote a research paper for this which dives deeper into my process in creating the model and its results/implications. \
[I published the paper on Medium](https://medium.com/@nicholas.kann/predicting-severity-in-california-traffic-collisions-27e8dec8bf3e).**

## 📚 Data 
The data is from the California Highway Patrol's Statewide Integrated Traffic Records System (CHP SWITRS), through [Alex Gude's Kaggle repository](https://www.kaggle.com/datasets/alexgude/california-traffic-collision-data-from-switrs).<br></br>
The chosen features were:
- longitude & latitude
- intersection (binary)
- road surface
- lighting
- state highway (binary)
- weather
- collision time & date

## 🛠️ Feature Transformation
- Categorical variables, namely 'weather_1', 'weather_2', 'lighting', and 'road_surface', were one-hot encoded.

- The 'collision_severity' variable was binary-encoded, with values of 'property damage only', 'pain', and 'other injury' assigned as 0, while 'severe injury' and 'fatal' were designated as 1.

- A binary 'weekend' feature was created from analyzing the 'collision_date' attribute.

- Addressing the cyclic nature of time-based features, such as 'collision_time' and 'collision_date', involved a distinct approach. Instead of conventional one-hot encoding, I utilized sine and cosine functions to ensure that all timepoints and dates were uniformly distributed in the transformed feature space. This cyclical approach was taken from [Satyam Kumar](https://towardsdatascience.com/stop-one-hot-encoding-your-time-based-features-24c699face2f).


## 📊 Results
##### *The table below displays the performance metrics of the various machine learning models used in predicting traffic collision severity.*
| Model                        | Accuracy | Precision | Recall | F1 Score |
|------------------------------|----------|-----------|--------|----------|
| Decision Tree                | 0.6217   | 0.0480    | 0.5179 | 0.0879   |
| Random Forest                | 0.6989   | 0.0619    | 0.5339 | 0.1109   |
| Naive Bayes                  | 0.8539   | 0.0636    | 0.2297 | 0.0997   |
| K-Nearest Neighbors          | 0.6831   | 0.0556    | 0.5007 | 0.1001   |
| Gradient Boosting            | 0.7406   | 0.0681    | 0.5020 | 0.1199   |
| XGBoost                      | 0.7209   | 0.0697    | 0.5618 | 0.1241   |
| LightGBM                     | 0.6199   | 0.0608    | 0.6786 | 0.1116   |

Although Naive Bayes had the best accuracy by a long shot, recall is more important in this case since recall is essentially the accuracy of predicting positive (severe) cases, and over-preparation in scenarios where predicting severe outcomes is crucial. So, LightGBM performed the best with a recall of 67.86%.

##### *The table below displays the classification report for the LightGBM model.*
|           | Precision | Recall | F1-Score | Support |
|-----------|-----------|--------|----------|---------|
| Non-Severe| 0.98      | 0.62   | 0.76     | 20647   |
| Severe    | 0.06      | 0.68   | 0.11     | 753     |
| Accuracy  |           |        | 0.62     | 21400   |
| Macro Avg | 0.52      | 0.65   | 0.43     | 21400   |
| Weighted Avg | 0.95   | 0.62   | 0.74     | 21400   |


## 🚀 Usage

To use this model, you can access the Jupyter Notebook file in the following link:

[Link to colab](https://colab.research.google.com/drive/1zUzP0hCZRbABcqPjjfxTiOp1XOc-un_8)

Feel free to explore and experiment with different algorithms, architectures, hyperparameters, and techniques to enhance the model's performance.

## 💡 Feedback

Although the model's performance is far from perfect and obviously would not be a reliable system for making critical decisions, it serves as a valuable starting point for understanding patterns and trends in the data. This analysis opens the door for iterative improvements, and your input can contribute significantly to refining the model.<br></br>
For any suggestions or questions, please email me at nicholas.kann@gmail.com. Your feedback is greatly appreciated!

## 🧑‍💻 Author
Nicholas Kann / [@butter-my-toast](https://github.com/butter-my-toast "butter-my-toast's github page")
