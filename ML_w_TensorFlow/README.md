### Neural Networks & Deep Learning

We are given data from an Audiobook app.

We want to build a Machine Learning algorithm based on our data that can predict if a customer is likely to make a purchase from the audiobook company again. We want to focus our marketing efforts on individuals likely to convert again in order to improve sales and profitability of the business.

#### The solution outlined:

1. Preprocessing. The dataset has been shuffled, balanced and split into training, validation and test follwing a 80-10-10 rule. Then, we have dataset in tensor-friendly format *.npz

- Dataset: [Audiobooks_data.csv
- Notebook: [Audiobooks_TensorFlow_Preprocessing.ipynb

2. The Model: a ML algorithm with TensorFlow

Notebook: [Audiobooks_TensorFlow_Model.ipynb](https://github.com/judithbaeta/data-science-101/blob/master/Audiobooks_TensorFlow_Model.ipynb)

- Input layer has 10 nodes

    - `book_length_overall` and `book_length_averge`: The overall book length is the sum of the lengths of purchases. The     average length is the sum divided by the number of purchases. For an individual that has made a single purchase, overall length = average length. The number of purchases is contained in this variable.
    - `price_overall` and `price_average`. Price is in dollars although that’s no relevant for the algorithm.
    - `review` is a boolean and shows if the customer left a review (1= left review, 0= didn’t). This metric shows engagement with the platform, the assumption is that a customer that left a review is more likely to convert again.
    - `review 10/10`: It measures the review of a customer from 1 to 10, yet another variable that is an average (across purchases). However, as in most marketplaces, most people left no review and this value is missing. We’ve filled those MV by the average review. Thus, for our ML algorithm, the average of 8.91= status quo. Review > 8.91 = above average “feelings" while < 8.81 indicates below average “feelings”.
    - `minutes_listened`: Total minutes listened. Another measure of engagement
    - `completion`: total minutes listened / book length_overall, assuming customers won’t re-listen to a book.
    - `support_request`: the number of support requests a person has opened (e.g. from forgotten password to assistance). Again a measure of engagement, the more support you’ve needed, the more likely you got fed up with the platform and abandoned, OR, contrarily, from using it you stepped upon different issues unlike someone who never opened the app.
    - `last visited minus purchase date`: difference between the last time a person interacted with the platform and the first purchase date. Another measure of engagement. The bigger the difference the better, a person that engages regularly with the platform. If the value is zero, we are sure the customer never accessed what he/she has bought and unlikely they will confer again.
    
- Targets: The data was gathered from the audiobook app. The inputs represent 2 years worth of engagement. We're doing supervised learning so we took an extra 6-month period of data to check conversion (targets), essentially whether the customer bought another book. It's a boolean, 1= the customer converted, 0= didn’t. Thus, the output layer has 2 output nodes as there are only two target possibilities, 0 and 1.

- Depth: 2 hidden layers
- Width: 50 hidden unites on each hidden layer. 50 provides enough complexity, and we don’t want to put too many units initially so we can complete the learning as fast as possible.
- Activation functions: we've chosen ReLu on the hidden layers and Softmax for the output layer (classifyier) 
- Optimizer: Adam
- Loss: Sparse Categorical Crossentropy to apply one-hot encoding to the targets
