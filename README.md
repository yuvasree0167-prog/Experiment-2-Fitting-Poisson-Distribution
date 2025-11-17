# Experiment-2-Fitting-Poisson-Distribution
Aim: 
To fit Poisson distribution for the arrival of objects per minute from the feeder. 
# Software required: 

Python and Visual Component Tool
# Theory: 

1. The Poisson distribution gives the probability of a number of events occurring in a fixed interval of time or space when events occur independently and at a constant average rate (λ).
2. The probability mass function (PMF) is:  
<img width="1171" height="73" alt="image" src="https://github.com/user-attachments/assets/e28da9e9-3b3f-4969-baa9-2ff06c3358ba" />
3. Here, λ = mean number of occurrences, and e = 2.718 (base of natural logarithm).
4. The mean and variance of a Poisson distribution are both equal to λ.
5. Applicable when events occur independently, singly, and at a constant rate.
# Algorithm
<img width="1144" height="412" alt="image" src="https://github.com/user-attachments/assets/6bf357bd-7ba2-4908-8c93-ef74e4747a4f" />

# Program
Name: YUVASREE S
Slot-name:3P1-1

import numpy as np
import math
import scipy.stats

# Input
L = [int(i) for i in input("Enter data: ").split()]
N = len(L)
M = max(L)

X = []
f = []

# Frequency calculation
for i in range(M + 1):
    c = 0
    for j in range(N):
        if L[j] == i:
            c += 1
    f.append(c)
    X.append(i)

sf = np.sum(f)

# Probability P(x)
p = []
for i in range(M + 1):
    p.append(f[i] / sf)

# Mean of Poisson distribution
mean = np.inner(X, p)

# Reset lists
p = []
E = []
xi = []

print("X   P(X=x)   Obs.Fr   Exp.Fr   xi")
print("-----------------------------------")

# Poisson probability, expected frequency & Chi-square term
for x in range(M + 1):
    px = math.exp(-mean) * (mean ** x) / math.factorial(x)
    p.append(px)

    exp_f = px * sf
    E.append(exp_f)

    xi_val = ((f[x] - exp_f) ** 2) / exp_f if exp_f != 0 else 0
    xi.append(xi_val)

    print("%2d   %.3f   %4d   %.2f   %.3f" %
          (x, px, f[x], exp_f, xi_val))

print("-----------------------------------")

# Chi-square
cal_chi2 = np.sum(xi)
print("Calculated value of Chi-square = %.4f" % cal_chi2)

# Table value (1% LOS)
table_chi2 = scipy.stats.chi2.ppf(1 - 0.01, df=M)
print("Table value of Chi square is 1%% level is %.4f" % table_chi2)

# Conclusion
if cal_chi2 < table_chi2:
    print("The given data CAN be fitted to Poisson Distribution at 1% LOS")
else:
    print("The given data CANNOT be fitted to Poisson Distribution at 1% LOS")
    
https://colab.research.google.com/drive/18iW8j5_KuycRt2zbG14p2f3-pK2UPv4_#scrollTo=cWhWifdWw7Bc





# Output
Enter data: 9 9 9 8 8 8 7 7 5 6 3 
X   P(X=x)   Obs.Fr   Exp.Fr   xi
-----------------------------------
 0   0.001      0   0.01   0.008
 1   0.005      0   0.06   0.060
 2   0.020      0   0.22   0.216
 3   0.047      1   0.52   0.453
 4   0.084      0   0.93   0.927
 5   0.121      1   1.33   0.083
 6   0.145      1   1.59   0.221
 7   0.149      2   1.64   0.081
 8   0.133      3   1.47   1.599
 9   0.106      3   1.17   2.854
-----------------------------------
Calculated value of Chi-square = 6.5026
Table value of Chi square at 1% level is  21.6660
The given data CAN be fitted to Poisson Distribution at 1% LOS



# Result
The Poisson Distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 

