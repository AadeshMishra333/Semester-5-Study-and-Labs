1. **For a logistic-regression model, how does cost(h(x), y) change with h(x), if y = 1?**
   - **Answer:** cost(h(x), y) = 0 when h(x) = 1

2. **A logistic-regression model is log(p/(1−p)) = −3 + 0.7X. If X increases by 2 units, by what factor are the odds of Y = 1 multiplied?**
   - **Answer:** e¹·⁴ ≈ 4.06

3. **A logistic regression model uses z = −1 + 0.8*x and p = 1/(1 + e⁻ᶻ). For x = 2, what is the predicted probability and class when the classification threshold is 0.5?**
   - **Answer:** p = 0.65, Class 1

4. **For a single logistic-regression training observation x = 3, y = 0 and the current model predicts p = 0.8, what must happen to β₁ after a gradient-descent update with a positive learning rate?**
   - **Answer:** β₁ decreases because the gradient is positive.

5. **Consider the simple linear regression model ŷ = w*x + b. For training data (1, 2) and (2, 3), initially w = 0 and b = 0, using SGD for two complete passes with α = 0.1, what are the final values of w and b?**
   - **Answer:** w = 0.9552, b = 0.6216

6. **An artificially intelligent car performs two tasks: I. It predicts how much to reduce its speed based on the distance from the car ahead. II. It decides whether to brake or not. Which algorithms are most suitable?**
   - **Answer:** Linear Regression for Task I and Logistic Regression for Task II

7. **For two observations with actual class y = 1, Model A predicts p = 0.60 and Model B predicts p = 0.90. Using a classification threshold of 0.5, which statement about their binary cross-entropy losses is correct?**
   - **Answer:** Model B has smaller loss; approximately 0.105 compared with 0.511 for Model A.

8. **In the Logistic Regression implementation, why is fit_transform() applied to X_train, while only transform() is applied to X_test?**
   - **Answer:** Because the mean and standard deviation should be learned from the training data, and the same learned scaling parameters should then be applied to the test data.

9. **In gradient descent, imagine you're blindfolded on a mountain trying to reach the bottom by feeling the slope under your feet and taking steps downhill. In this analogy, what does the valley represent?**
   - **Answer:** The error or loss in model predictions

10. **During training, a model uses gradient descent to minimize its cost function. The cost values over successive iterations are 4.2, 2.8, 1.9, 2.6, 4.1, 6.8. What is the most likely explanation?**
    - **Answer:** The learning rate is too large, causing the updates to overshoot the minimum and eventually diverge.
