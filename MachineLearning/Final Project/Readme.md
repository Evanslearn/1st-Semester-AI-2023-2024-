# This ipynb was developed in Google Colab, for the Final Project of the Machine Learning Postgraduate Course of Artificial Inteligence Master of CSD AUTH.
## The problem that I modeled here is an attempt to learn the rock-paper-scissors game.
* The enemy playes first, so we see an image of an action (rock/paper/scissors)
* Our model then tries to select the optimal action, which would make it win (so if the enemy played rock, then our model should choose paper)
<br/>

### I trained my model using this dataset: https://www.kaggle.com/datasets/drgfreeman/rockpaperscissors
* This dataset contains a little over 700 images of each action (700+ for rock, 700+ for paper, 700+ for scissors), which are 200x300 pixels each.
* I used 80% of the data as the train set, and 20% as the test set
### I also tested my model at this dataset: https://www.kaggle.com/datasets/glushko/rock-paper-scissors-dataset
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
* If our model wins, we get 2 points
* If our model gets a draw, we get 1 point
* If our model loses, we get no points
