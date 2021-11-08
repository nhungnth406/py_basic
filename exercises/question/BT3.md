1/ Rondo is in the market for a new car. He has narrowed his search down to 2 models.</br>
Model A costs $32,000 and Model B costs $28,000. With both cars he plans to pay cash and own them for 4 years before trading in for a new car. </br>
His research indicates that the trade in value for Model A after 4 years is 60% of the initial purchase price, while the trade in value for Model B is 45%. </br>
The interest rate is 5%. For simplicity assume that operating and maintenance costs for the models are identical. </br>
Which model is the better decision and how much "cheaper" is it than the alternative?

----------------
My solution
``` python
import numpy_financial as npf

#Price A after 4 years
NCA = 32000 - 32000*0.6

#Price B after 4 years
PB = 28000 - 28000*0.45

#Future value of $4000 savings if choose B
FVSB = npf.fv(0.05,4,0,-4000) - 4000

##Net cost B after 4 years
NCB = PB - FVSB

delta = round((NCA - NCB),2)
if delta < 0:
    print("Model A is better decision, cheaper than $", abs(delta))
else:
    print("Model B is better decision, cheaper than $", abs(delta))
  ```
 =====================================================================================
 
 
 2/ Two years ago Abilia purchased a $10,000 car; she paid $2000 down and borrowed the rest. She took a fixed rate 60-month installment loan at a stated rate of 8% per year.</br>
Interest rates have fallen during the last two years and she can refinance her car by borrowing the amount she still owes on the car at a new fixed rate of 6% per year for 3 years. </br>
a/ How much will she save per month for the next three years if she decides to refinance? </br>
b/ Whatif the fee to refinance her loan is $100? (Should she refinance the remaining balance? How much would she save/lose if she decided to refinance?,...)

----------------
My solution: 
```python
import numpy_financial as npf
#a
print("a/")
PV = 10000 - 2000
print("PV = $", PV)
print("nper =", 60, "months")
print("rate =", 0.08)
a = npf.pmt(0.08/12, 60, -PV)
print("PMT = $", a)
b = npf.pv(0.08/12, 36, -a)
print("At Third Year, PV1 = $", b)
c = npf.pmt(0.06/12, 36, -b)
print("PMT1 = $", c)
s1 = a - c
print("She will save",round(s1,2), "$ per month for the next three years if she decides to refinance")

#b
print("b/")
#pv of saving 
pvs = npf.pv(0.06/12,36,-s1)
s2 = round((pvs - 100),2)
if s2 > 0:
    print("Yes, gain $",abs(s2))
else:
    print("No, lose $",abs(s2))
```
