# Homework 2

## Submission instructions

* Expected time commitment: 5 hrs

* Carmen submission:
Submit one .zip file named HW2_programming_name_number.zip (e.g., HW2_programming_chao_209.zip), which contains
  - your completed python script `LR.py`
  - your 4 generated results: `linear_1.png`, `quadratic_2.png`, `Results_linear_1.npz`, and `Results_quadratic_2.npz`
  - a `collaboration.txt` which lists with whom you have discussed the homework (see more details below).

* Collaboration: You may discuss the homework with your classmates. However, you need to write your own solutions and submit them separately. In your submission, you need to list with whom you have discussed the homework in a .txt file `collaboration.txt`. Please list each classmate’s name and name.number (e.g., Wei-Lun Chao, chao.209) as a row in the .txt file. That is, if you discussed with two classmates, your .txt file will have two rows. If you did not discuss with your classmates, just write "no discussion" in `collaboration.txt`. Consult the syllabus for what is and is not an acceptable collaboration.

## Implementation instructions

* You will see three python scripts: `LR.py`, `feature_normalization.py`, and `numpy_example.py`. You will also see `collaboration.txt`.

* You will see a `data` folder, which contains `mnist_test.csv`, `Linear.npz`, `Quadratic.npz`, and `Swiss_Roll.npz`.

* You will see a folder `for_display`, which simply contains some images used for display here.

* Use python3 and write your own solutions from scratch.

* **Caution! python and NumPy's indices start from 0. That is, to get the first element in a vector, the index is 0 rather than 1.**

* We note that, the provided commands are designed to work with Mac/Linux with Python version 3. If you use Windows, we recommend that you run the code in the Windows command line (CMD). You may use `py -3` instead of `python3` to run the code. You may use editors like PyCharm to write your code.

* **Caution! Please do not import packages that are not listed in the provided code. Follow the instructions in each question strictly to code up your solutions.** Do not change the output format. Do not modify the code unless we instruct you to do so. (You are free to play with the code but your submitted code should not contain those changes that we do not ask you to do.) A homework solution that does not match the provided setup, such as format, name, initializations, etc., will not be graded. It is your responsibility to make sure that your code runs with the provided commands and scripts.

## Installation instructions

* You will be using [NumPy] (https://numpy.org/), and your code will display your results with [matplotlib] (https://matplotlib.org/). If your computer does not have them, you may install with the following commands:
  - for NumPy: <br/>
    do `sudo apt install python3-pip` or `pip3 install numpy`. If your are using Windows command line, you may try `setx PATH "%PATH%;C:\Python34\Scripts"`, followed by `py -3 -mpip install numpy`.

  - for matplotlib: <br/>
    do `python3 -m pip install -U pip` and then `python3 -m pip install -U matplotlib`. If you are using the Windows command line, you may try `py -3 -mpip install -U pip` and then `py -3 -mpip install -U matplotlib`.

# Introduction

In this homework, you are to implement linear regression and apply your completed algorithm to multiple different datasets to see their pros and cons.

You will play with simple linear and quadratic data (x-axis is the feature variable; y-axis is the real-value label; each point is a data instance: red for training and blue for testing) and some other toy datasets.

![Alt text](https://github.com/pujols/OSU_CSE_3521_2021AU/blob/main/HW_2_Porgramming_Set/HW_2_Programming/for_display/linear_1.png)

![Alt text](https://github.com/pujols/OSU_CSE_3521_2021AU/blob/main/HW_2_Porgramming_Set/HW_2_Programming/for_display/quadratic_2.png)


# Question 0: Exercise

* You will use [NumPy] (https://numpy.org/) extensively in this homework. NumPy a library for the Python programming language, adding support for large, multi-dimensional arrays and matrices, along with a large collection of high-level mathematical functions to operate on these arrays. NumPy has many great functions and operations that will make your implementation much easier.

* If you are not familiar with Numpy, we recommend that you read this [tutorial] (https://cs231n.github.io/python-numpy-tutorial/) or some other tutorials online, and then play with some code to get familiar with it.

* We have provided some useful Numpy operations that you may want to use in `numpy_example.py`. You may want to comment out all the lines first, and execute them one by one or in a group to see the results and the differences. You can run the command `python3 numpy_example.py`.

* We also provide another python script `feature_normalization.py`, which will guide you through L2 normalization, covariance matrices, z-score, and whitening. You may find some code here helpful for your implementation. You can run the command `python3 feature_normalization.py`.

* In `LR.py`, we also provide some more instructions and hints for what functions or operations you may want to use.

* Caution! python and NumPy's indices start from 0. That is, to get the first element in a vector, the index is 0 rather than 1.

# Linear regression (25 pts)
* You will implement linear regression in this question. You are to amend your implementation into `LR.py`.

* There are many sub-functions in `LR.py`. You can ignore all of them but `def linear_regression(X, Y)` and `def main(args)`. In `main(args)`, you will see a general pipeline of machine learning: <br/>
  - Loading data: `X_original, Y = data_loader(args)`, in which `X_original` is a 1-by-N matrix (numpy array) and each column is a data instance. You can type `X_original[:, 0]` to extract the "first" data instance from `X_original`. (Caution! python and numpy's indices start from 0. That is, to get the first element in a vector, the index is 0 rather than 1.) <br/>
  - Feature transform: `X = polynomial_transform(np.copy(X_original), args.polynomial)` extends each column of `X_original` to its polynomial representation. For example, given a scalar x, this transform will extends it to [x, x^2, ..., x^(args.polynomial)]^T.
  - Learning patterns: `w, b = linear_regression(X, Y)`, in which the code takes `X` and the desired labels `Y` as input and output the weights `w` and the bias `b`.
  - Apply the learned patterns to the data: `training_error = np.mean((np.matmul(w.transpose(), X) + b - Y.transpose()) ** 2)` and `test_error = np.mean((np.matmul(w.transpose(), X_test) + b - Y_test.transpose()) ** 2)` compute the training and test error.

## Coding (15/25 pts):

You have one part to implement in `LR.py`:

* The function `def linear_regression(X, Y)`: please go to the function and read the input format, output format, and the instructions carefully. You can assume that the actual inputs will follow the input format, and your goal is to generate the required numpy arrays (`w` and `b`), the weights and bias of linear regression. Please make sure that your results follow the required numpy array shapes. You are to implement your code between `### Your job starts here ###` and `### Your job ends here ###`. You are free to create more space between those two lines: we include them just to explicitly tell you where you are going to implement.

## Auto grader:

* You may run the following command to test your implementation<br/>
`python3 LR.py --data simple --auto_grade`<br/>
Note that, the auto grader is to check your implementation semantics. If you have syntax errors, you may get python error messages before you can see the auto_graders' results.

* Again, the auto_grader is just to simply check your implementation for a toy case. It will not be used for your final grading.

## Play with different datasets (Task 1 - linear data, 5/25 pts):

* Please run the following command<br/>
`python3 LR.py --data linear --polynomial 1 --display --save`<br/>
This command will run linear regression on a 1D linear data (the x-axis is the feature and the y-axis is the label). You will see the resulting `w` and `b` being displayed in your command line. You will also see the training (on red points) and test error (on blue points).

* The code will generate `linear_1.png` and `Results_linear_1.npz`, which you will include in your submission.

* You may play with other commands by (1) removing `--save` (2) changing the `--polynomial 1` to a non-negative integer (e.g, 2, 3, ..., 13). You will see that, while larger values lead to smaller training errors, the test error is not necessarily lower. For very large value, the test error can go very large.

## Play with different datasets (Task 2 - quadratic data, 5/25 pts):

* Please run the following command<br/>
`python3 LR.py --data quadratic --polynomial 2 --display --save`<br/>
This command will run linear regression on a 1D quadratic data (the x-axis is the feature and the y-axis is the label). The code will produce polynomial = 2 representation for the data (i.e., `X` becomes 2-by-N). You will see the resulting `w` and `b` being displayed in your command line. You will also see the training (on red points) and test error (on blue points).

* The code will generate `quadratic_2.png` and `Results_quadratic_2.npz`, which you will include in your submission.

* You may play with other commands by (1) removing `--save` (2) changing the `--polynomial 2` to a non-negative integer (e.g, 1, 3, ..., 13). You will see that, while larger values lead to smaller training error, the test error is not neccessarily lower. For very large value, the test error can go verly large.

## What to submit:

* Your completed python script `LR.py`

* Your 4 generated results for Question 2: `linear_1.png`, `quadratic_2.png`, `Results_linear_1.npz`, and `Results_quadratic_2.npz`
