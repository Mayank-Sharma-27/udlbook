### Q1 : What kind of mapping from input to output would be created if the activation
function in equation 3.1 was linear so that a[z] = ψ0 + ψ1z? What kind of mapping would be
created if the activation function was removed, so a[z] = z?

Ans : It should behave like a simple linear model.

I verified with Chatgpt the answer seems to be correct

This is the answer that chatGpt gave me


Final Answer
Replacing ReLU with a linear activation results in a network that is still only capable of learning linear transformations.
Removing the activation function entirely makes the network behave like a single linear layer, regardless of depth.
In both cases, the network loses its ability to model complex, non-linear relationships, which is the key power of deep learning.


### Q2: Problem 3.2 **For each of the four linear regions in figure 3.3j, indicate which hidden units are
inactive and which are active (i.e., which do and do not clip their inputs)?**
The region is inactive if the pre-activation function \( \text{pre}_i \leq 0 \).

### **Short Summarized Answer**
| Region  | \( \text{act}_1 \) | \( \text{act}_2 \) | \( \text{act}_3 \) |
|---------|-----------------|-----------------|-----------------|
| **1** (leftmost)  | ❌ Inactive | ❌ Inactive | ❌ Inactive |
| **2** | ✅ Active | ❌ Inactive | ❌ Inactive |
| **3** | ✅ Active | ✅ Active | ❌ Inactive |
| **4** (rightmost) | ✅ Active | ✅ Active | ✅ Active |

### **Explanation**
We are given a piecewise linear model with three hidden units, each applying a **ReLU activation function**:

\[
\text{ReLU}(z) = \max(0, z)
\]

The outputs of these hidden units are weighted and summed to compute the final output:

\[
y = \phi_0 + w_{\text{act}_1} + w_{\text{act}_2} + w_{\text{act}_3}
\]

where:

\[
\begin{aligned}
\text{pre}_1 &= \theta_{10} + \theta_{11} x \\
\text{pre}_2 &= \theta_{20} + \theta_{21} x \\
\text{pre}_3 &= \theta_{30} + \theta_{31} x
\end{aligned}
\]

After applying **ReLU activation**, the activations become:

\[
\begin{aligned}
\text{act}_1 &= \max(0, \text{pre}_1) \\
\text{act}_2 &= \max(0, \text{pre}_2) \\
\text{act}_3 &= \max(0, \text{pre}_3)
\end{aligned}
\]

Then, each activation is weighted:

\[
\begin{aligned}
w_{\text{act}_1} &= \phi_1 \cdot \text{act}_1 \\
w_{\text{act}_2} &= \phi_2 \cdot \text{act}_2 \\
w_{\text{act}_3} &= \phi_3 \cdot \text{act}_3
\end{aligned}
\]

#### **Goal: Determine Active/Inactive Units in Four Linear Regions**
Figure **3.3j** divides the input space into **four regions**. Each region corresponds to a different combination of hidden units being **active (output > 0)** or **inactive (output = 0)**.

#### **Step 1: Identify Activation Boundaries**
Each pre-activation equation \( \text{pre}_i = \theta_{i0} + \theta_{i1} x \) defines a threshold where the corresponding **hidden unit turns on or off**:
- **If \( \text{pre}_i > 0 \)** → \( \text{act}_i \) is **active**.
- **If \( \text{pre}_i \leq 0 \)** → \( \text{act}_i \) is **inactive (zero output)**.

#### **Step 2: Define the Four Linear Regions**
Each region is a section of the \( x \)-axis where a unique subset of hidden units are **active**. The possible cases are:

1. **Region 1: \( x \) is very small (leftmost region)**  
    - \( \text{pre}_1 \leq 0 \Rightarrow \) **Inactive**
    - \( \text{pre}_2 \leq 0 \Rightarrow \) **Inactive**
    - \( \text{pre}_3 \leq 0 \Rightarrow \) **Inactive**
    - **All hidden units are inactive** → \( y = \phi_0 \).

2. **Region 2: \( x \) crosses the first threshold**  
    - \( \text{pre}_1 > 0 \Rightarrow \) **Active**
    - \( \text{pre}_2 \leq 0 \Rightarrow \) **Inactive**
    - \( \text{pre}_3 \leq 0 \Rightarrow \) **Inactive**
    - **Only Hidden Unit 1 is active** → \( y = \phi_0 + \phi_1 \text{act}_1 \).

3. **Region 3: \( x \) crosses the second threshold**  
    - \( \text{pre}_1 > 0 \Rightarrow \) **Active**
    - \( \text{pre}_2 > 0 \Rightarrow \) **Active**
    - \( \text{pre}_3 \leq 0 \Rightarrow \) **Inactive**
    - **Hidden Units 1 and 2 are active** → \( y = \phi_0 + \phi_1 \text{act}_1 + \phi_2 \text{act}_2 \).

4. **Region 4: \( x \) crosses the third threshold (rightmost region)**  
    - \( \text{pre}_1 > 0 \Rightarrow \) **Active**
    - \( \text{pre}_2 > 0 \Rightarrow \) **Active**
    - \( \text{pre}_3 > 0 \Rightarrow \) **Active**
    - **All three hidden units are active** → \( y = \phi_0 + \phi_1 \text{act}_1 + \phi_2 \text{act}_2 + \phi_3 \text{act}_3 \).

🚀 **Key Takeaway:**  
- **Each decision boundary "turns on" a new hidden unit** as \( x \) increases.
- This structure allows **piecewise linear functions** to be formed.
- Without **ReLU**, all units would always be active, reducing expressiveness.

Here's the plot of the output \( y(x) \) based on the activations of the hidden units and the weights \( \phi_0, \phi_1, \phi_2, \phi_3 \). 

![public/ans_2.png](/public/ans_2.png)

As you can see:
- **Before the first threshold** (leftmost region), the output \( y(x) \) is flat and determined only by \( \phi_0 \).
- Once the hidden units start activating as \( x \) crosses the decision boundaries, the output starts changing dynamically based on the respective activations.

This shows how the output is dependent on \( \phi_0 \) in the leftmost region, and then it gradually becomes influenced by the activations of the hidden units as you move to the right.  

//Todo

### Problem 3 Derive expressions for the positions of the “joints” in function in figure 3.3j interms of the ten parameters φ and the input x. Derive expressions for the slopes of the four linear regions.

The slope will be basaed on the above answer2

Region 1: All hidden units are inactive, ( y = \phi_0 ).
Region 2: Only Hidden Unit 1 is active, ( y = \phi_0 + \phi_1 \text{act}_1 ).
Region 3: Hidden Units 1 and 2 are active, ( y = \phi_0 + \phi_1 \text{act}_1 + \phi_2 \text{act}_2 ).
Region 4: All three hidden units are active, ( y = \phi_0 + \phi_1 \text{act}_1 + \phi_2 \text{act}_2 + \phi_3 \text{act}_3 ).


First region:

None of the hidden units are active.
Slope: ( 0 ).

Second region:
Only the third hidden unit is active.
Slope: ( \theta_{31} \phi_3 ).

Third region:
The first and third hidden units are active.
Slope: ( \theta_{11} \phi_1 + \theta_{31} \phi_3 ).

Fourth region:
The first, second, and third hidden units are active.
Slope: ( \theta_{11} \phi_1 + \theta_{21} \phi_2 + \theta_{31} \phi_3 ).