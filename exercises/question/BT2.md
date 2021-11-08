Q1: Input D.O.B. Calculate days remaining to a birthday.

-----------------
My solution:
```python
import datetime
from datetime import date

next = True
while next == True:
    d1 = datetime.datetime.strptime(input('Input date (day/month): '), '%d/%m')
    d1 = d1.date()
    d1 = d1.replace(year = date.today().year)
    print("Birthday this year:", d1.strftime('%B %d, %Y'))
    d2 = date.today()
    delta = d1 - d2
    delta = delta.days
    if d1.day == d2.day and d1.month == d2.month:
        print('Today (' + d1.strftime('%B %d, %Y') +  ') is your birthday')
    elif d1 < d2:
        d1 = d1.replace(year = date.today().year + 1)
        delta = d1 - d2
        print('Time to next birthday:', delta, 'day(s)')
    else:
        print('Time to next birthday:', delta, 'day(s)')
    while 1==1:
        a = input('Continue (Y/N)? :')
        if a == 'N' or a =='n':
            next = False
            break
        elif a == 'Y' or a== 'y':
            next = True
            break
        else:
            print("Invalid. Check again!")
```
=============================================

Q2: Create a triangle class, class triangle has properties that are 3 sides of the triangle, 2 methods are to calculate the perimeter and area of the triangle, 1 attribute counts how many triangles have been created?

-----------------
My solution:
```python
import math
class Triangle:
    total_triangle = 0
    def __init__(self,a,b,c):
        self.sideA = a   
        self.sideB = b  
        self.sideC = c 
        if (self.sideA + self.sideB > self.sideC) and (self.sideA + self.sideC > self.sideB) and (self.sideB + self.sideC > self.sideA):                
            self.is_valid = True
            Triangle.total_triangle = Triangle.total_triangle + 1
        else:
            self.is_valid = False

    def calculate_perimeter(self):
        perimeter = self.sideA+self.sideB+self.sideC
        return round(perimeter,2)
    def calculate_area(self):
        p = (self.sideA+self.sideB+self.sideC)/2
        area = math.sqrt(p*(p-self.sideA)*(p-self.sideB)*(p-self.sideC))
        return round(area,2)
          
next = True
while next == True:
    a, b, c = map(float, input("Input 3 sides of triangle: ").split())
    triangle = Triangle(a,b,c)
    
    if triangle.is_valid == True:
        print("Perimeter of triangle",Triangle.total_triangle,"is:",triangle.calculate_perimeter())
        print ("Area of triangle",Triangle.total_triangle, "is:", triangle.calculate_area())
    else: 
        print("Not 3 sides of triangle")

    while 1==1:
        a = input('Continue (Y/N)?:')
        if a == 'N' or a =='n':
            next = False
            break
        elif a == 'Y' or a== 'y':
            next = True
            break
        else:
            print("Error: Invalid!")
```
