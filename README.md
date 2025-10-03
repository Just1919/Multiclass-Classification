# Multiclass-Classification

## Multiclass Classification


Now we move on to multiclass classification, where there are n possible outcomes instead of just two.
A classic example is optical character recognition: analyzing a handwritten digit and predicting whether it’s 0 through 9. Another example is face recognition, where a photo is matched against a model trained to identify hundreds of individuals.

Almost everything you learned about binary classification also applies to multiclass classification. In Scikit-learn, any classifier designed for binary problems can also be used for multiclass tasks. This is a major advantage, because many libraries require you to write extra code or use specialized methods to extend algorithms like logistic regression to handle multiple classes. Scikit takes care of this automatically.

For logistic regression, Scikit-learn uses two possible strategies to handle multiclass problems (controlled by the multi_class parameter in LogisticRegression, with the default being 'auto'):

1. Multinomial logistic regression: replaces the logistic (sigmoid) function with a softmax function, producing one probability per class.

2. One-vs-Rest (OvR) / One-vs-All: trains n binary classifiers (one per class). Each model distinguishes one class against all others. At prediction time, the input is evaluated across all n models, and the class with the highest probability is selected.






The one-vs-rest (OvR) approach works well with logistic regression, but for algorithms that can only handle binary classification, Scikit-learn often uses a one-vs-one (OvO) strategy instead. For example, when using the SVC class (Support Vector Machine), Scikit automatically builds a separate model for every possible pair of classes. If your dataset has four classes, this results in six models being created behind the scenes.

You don’t need to worry about these details to train a multiclass classifier, but they help explain why some models consume more memory and take longer to train than others. Certain algorithms, such as Random Forests and Gradient Boosting Machines (GBMs), support multiclass classification natively. For others, Scikit-learn takes care of the extra work transparently so that you don’t have to.

In short: all Scikit-learn classifiers can handle both binary and multiclass classification, which keeps your code simple and lets you focus on building and training your models rather than dealing with the algorithm’s internal mechanics.

### Building a Digit Recognition Model



Want to try out multiclass classification in practice? Let’s build a model that looks at scanned images of handwritten digits and predicts which digit (0–9) each image represents. The U.S. Postal Service developed a similar system years ago to recognize handwritten ZIP codes as part of their mail-sorting automation.

For our example, we’ll use a dataset included with Scikit-learn: the Optical Recognition of Handwritten Digits dataset from the University of California, Irvine. It contains nearly 1,800 digit samples, each represented as an 8 × 8 grid of values ranging from 0 to 16, where higher values correspond to darker pixels.

We’ll apply logistic regression to make predictions with this data.
