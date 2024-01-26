# This ipynb was developed in Google Colab, for the Final Project of the Machine Learning Postgraduate Course of Artificial Inteligence Master of CSD AUTH.
## The problem that I modeled here is an attempt to learn the rock-paper-scissors game.
* The enemy playes first, so we see an image of an action (rock/paper/scissors)
* Our model then tries to select the optimal action, which would make it win (so if the enemy played rock, then our model should choose paper)
<br/>

# To run this ipynb:
* create folders 'rock', 'scissors', 'paper', to accomodate the training data set
  * Upload the appropriate images in each folder
* create folders 'rock_test', 'scissors_test', 'paper_test', to use the external test set.
  * Upload the appropriate images in each folder
* Run all cells
<br/>

## I trained my model using this dataset: https://www.kaggle.com/datasets/drgfreeman/rockpaperscissors
* This dataset contains a little over 700 images of each action (700+ for rock, 700+ for paper, 700+ for scissors), which are 200x300 pixels each.
* I used 80% of the data as the train set, and 20% as the test set
## I also tested my model at this dataset: https://www.kaggle.com/datasets/glushko/rock-paper-scissors-dataset
* This dataset also contains more than 700 images of each action, which are 300x300 pixels each.
* I only used the test set, which contained 176paper, 176 scissors, 188rock images.
<br/>

## Data pre-processing:
* After reading the images, I convert them to grayscale, then I keep only 20x30 pixels
* Then, I scale the images to [0,1] (normalization using the min and the max value)
* I encode the class labels as:
  * rock = 0
  * scissors = 1
  * paper = 2
<br/>

## While testing the model, I added some pre-processing logic to the input image:
* With probability $p_1=0.5$, apply Vertical Flip
* With probability $p_2=0.5$, applay Horizontal Flip
* Adding noise to each pixel, with $\mu = 0, \sigma = 255 \cdot 0.05$. Given that we normalize the pixels, the standard deviation is also adjusted (255 holds for non-normalized images)
* I also add a $45^o$ degrees rotation
<br/>

## Then, the model receives the image, predicts the class label, and plays the appropriate action that would win. For every repetition, our model bets 1 point.
* If our model wins, we get 2 points (so, we have gained 1 point)
* If our model gets a draw, we get 1 point (so, we have not gained anything)
* If our model loses, we get no points (so, we have lost a point)
<br/>

# RESULTS:
## CNN:
* Best achieved Accuracy in the internal test set: This occured when applying no pre-processing steps, and the achieved accuracy was 97.53%. The line-plot of gain looks like this: <br/>
![image](https://github.com/Evanslearn/1st-Semester-AI-2023-2024-/assets/104510165/fa87ed7a-47f4-4cf3-8aca-a98724585f23)
* Best achieved Accuracy in the EXTERNAL test set: This occured when applying only the noise pre-processing step, and the achieved accuracy was 40.35%. The line-plot of gain looks like this: <br/>
![image](https://github.com/Evanslearn/1st-Semester-AI-2023-2024-/assets/104510165/155d07c9-6cfa-4532-a390-f69e7bf07251)

## SVM:
* Best achieved Accuracy in the internal test set: This occured when applying no pre-processing steps, or only the noise pre-processing step, and the achieved accuracy was 92.05%. The line-plot of gain looks like this: <br/>
![image](https://github.com/Evanslearn/1st-Semester-AI-2023-2024-/assets/104510165/6220a066-0532-42d2-ac7c-ec8850a4798f)
* Best achieved Accuracy in the EXTERNAL test set: This occured when applying all pre-processing steps, and the achieved accuracy was 33.52%. The line-plot of gain looks like this: <br/>
![image](https://github.com/Evanslearn/1st-Semester-AI-2023-2024-/assets/104510165/247eae90-b474-4bf8-93dc-bc65001f9e6e)
<br/>

<b>I also tried NN, kNN, RF in the internal train/test set, to see what test set accuracy they yield.</b>
## NN:
* Internal Test Set Accuracy: 76.58 %
## kNN:
* Internal Test Set Accuracy: 89.53 %
## RF:
* Internal Test Set Accuracy: 69.69 %

# CONCLUSION:
## I have chosen CNN as my best model, although the accuracy in the external set is not as hope as I would have liked. (max 40.35%).<br/>
## I have also tried SVM model, but the highest achieved accuracy was 33.52%
## I also tried NN, kNN, RF algorithms in the internal test set, but they did not prove to be as successful. (kNN did have good accuracy, but not as high as SVM or CNN)
* I believe the accuracy is not that great in the external test set, because the images had dimensions 300x300, and we rescaled them to 20x30, thus distorting them.
* The other explanation is that the accuracy dropped in the external test set, because they were not clear images of only an action (rock/scissors/paper) - they also contained a face and objects.
