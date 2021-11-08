1/ Effective annual interest rate (EAR) = (1 + NominalRate/NPer)^NPer -1 <br/>
NominalRate = ((EAR + 1)^(1/NPer) - 1) * NPer

Viết 2 hàm: EAR và NominalRate. Thử chạy hàm EAR với các tham số vào: NominalRate = 10%, NPer = 12; rồi chạy hàm NominalRate với tham số vào là giá trị EAR vừa mới tính. Làm tròn 2 chữ số sau phần thập phân.
### <h5>Màn hình kết quả:</h5>
![Image of kq1](https://github.com/nhungnth406/py_basic/blob/main/exercises/img/BT1-1.png)
-----------------
My solution:
```python
def CalEAR(NR, NPer):
    NR = NR/100
    return (1+NR/NPer)**NPer - 1

def CalNOM(EAR,NPer):
    return (((EAR + 1)**(1/NPer)) - 1) * NPer

EAR = CalEAR(10,12)
NOM = CalNOM(EAR,12)
print('EAR = {0:.2f}%'.format(EAR*100))
print('Nominal Rate = {0:.2f}%'.format(NOM*100))
```
=================================================

2/ FutureValue(InterestRate, NumberOfPeriod, Payment, PresentValue, Type)
### <h5>Màn hình kết quả:</h5>
![Image of kq1](https://github.com/nhungnth406/py_basic/blob/main/exercises/img/BT1-2.png)
-----------------
My solution:
```python
# FV, PV, r, nper, pmt
#Interest Rate = r/k (r: Nominal Rate, k: số kỳ trong năm) 
#Type: 0 - nếu pmt cuối kỳ, 1 - nếu pmt đầu kỳ
def FutureValue(r, nper, pmt, PV, Type):
 return -(PV*(1+r)**nper + pmt*(1 + r*Type)/r*((1 + r)**nper - 1))
print(FutureValue(0.1,4,-10,-100,0))
print(FutureValue(0.1,4,-10,-100,1))
print(FutureValue(0.1,4,10,-100,0))
print(FutureValue(0.1,4,10,-100,1))
print(FutureValue(0.1,4,-10,100,0))
print(FutureValue(0.1,4,10,100,1))
```
=================================================

3/ Cho danh mục đầu tư (Portfolio) gồm các chứng khoán với mã (Code), số lượng (Quantity), giá mua (AskPrice) lần lượt là

TCB, MSN,  POW, VNM, FPT, HPG, VCB, GAS
1200, 2350, 980, 1560, 1840, 1590, 2030, 1670
39.6, 87.6, 13.45, 100.6, 80.7, 45.9, 95.5, 90.1

a/ Tạo biến Portfolio (kiểu dữ liệu Dictionary) với danh mục đầu tư đó

Giả sử sau một thời gian bán với giá (BidPrice) lần lượt  là:

41.5, 89.3, 14.1, 102.7, 84.2, 47.8, 97.4, 92.8

b/ Tính
NetIncome ( = (BidPrice - AskPrice)*Quantity
EPS (Earning Per Share) ( = NetIncome/Quantity = BidPrice - AskPrice)
PoE (P on E: P/E =  BidPrice/EPS) của từng cổ phiếu 
của từng mã rồi đưa kết quả vào Portfolio

c/ Dùng input để nhập mã cổ phiếu rồi hiện all thông tin ở trên của cổ phiếu đó
### <h5>Màn hình kết quả:</h5>
![Image of kq1](https://github.com/nhungnth406/py_basic/blob/main/exercises/img/BT1-3c.png)
-----------------
My solution:
```python 
#### Dictionary
portfolio={
    "stock1":{
        "Code":"TCB",
        "Quanity":1200,
        "Askprice": 39.6,
        "Bidprice":41.5
        
    },
     "stock2":{
        "Code":"MSN",
        "Quanity":2350,
        "Askprice": 87.6,
        "Bidprice":89.3
    },
     "stock3":{
        "Code":"TCB",
        "Quanity":1200,
        "Askprice": 39.6,
        "Bidprice":14.1
         
    },
    "stock4":{
        "Code":"VNM",
        "Quanity":1560,
        "Askprice": 100.6,
        "Bidprice":102.7
    },
    "stock5":{
        "Code":"FPT",
        "Quanity":1840,
        "Askprice": 80.7,
        "Bidprice":84.2
        
    },
    "stock6":{
        "Code":"HPG",
        "Quanity":1590,
        "Askprice": 45.9,
        "Bidprice":47.8
    },
    "stock7":{
        "Code":"VCB",
        "Quanity":2030,
        "Askprice": 95.5,
        "Bidprice":97.4
        
    },
    "stock8":{
        "Code":"GAS",
        "Quanity":1670,
        "Askprice": 90.1,
        "Bidprice":92.8
    }
}
stock=str(input("Which code you want to find?:"))
for x in portfolio.values():
    netincome=x.get("Quanity")*(x.get("Bidprice")-x.get("Askprice"))
    x.setdefault("NetIncome",round(netincome,2))
    EPS=netincome/float(x.get("Quanity"))
    x.setdefault("EPS",round(EPS,2))
    PoE=x.get("Bidprice")/EPS
    x.setdefault("PoE",round(PoE,2))
    if stock==x.get("Code"):
        print(x)

#### Mảng
portfolio = {
"Code" : ["TCB", "MSN", "POW", "VNM", "FPT", "HPG", "VCB", "GAS"],
"Quantity" : [1200, 2350, 980, 1560, 1840, 1590, 2030, 1670],
"AskPrice" : [39.6, 87.6, 13.45, 100.6, 80.7, 45.9, 95.5, 90.1]
}
portfolio['BidPrice'] = [41.5, 89.3, 14.1, 102.7, 84.2, 47.8, 97.4, 92.8]
listNI = []
listEPS = []
listPoE = []
for i in range(0,len(portfolio.get("Code"))):
  NetIncome = (portfolio.get('BidPrice')[i] - portfolio.get('AskPrice')[i])* (portfolio.get('Quantity')[i])
  listNI.append(round(NetIncome,2))
  EPS = portfolio.get('BidPrice')[i] - portfolio.get('AskPrice')[i]
  listEPS.append(round(EPS,2))
  portfolio["NetIncome"] = listNI
  portfolio["EPS"] = listEPS
  PoE = (portfolio.get('BidPrice')[i]) / (portfolio.get('EPS')[i])
  listPoE.append(round(PoE,2))    
  portfolio["PoE"] = listPoE
      
stock=str(input("Which code you want to find?:"))
for i in range(0,len(portfolio.get("Code"))):
    if stock == portfolio.get("Code")[i]:
        print('Input Code:',stock)
        print( 
        'Quantity:',portfolio.get("Quantity")[i], 
        ', AskPrice:',portfolio.get("AskPrice")[i],
        ", BidPrice:",portfolio.get("BidPrice")[i], 
        ", NetIncome:",portfolio.get("NetIncome")[i], 
        ", EPS:", portfolio.get("EPS")[i],
        ", PoE:",portfolio.get("PoE")[i])
  ```




