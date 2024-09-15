import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import random as rd
from random import sample
import math
dataset=pd.read_excel(r'C:\Users\user\Desktop\KNN project\Rice_Cammeo_Osmancik.xlsx')
'''number of columns and rows in excel file'''
#print("number of columns is",len(dataset.columns))
#print("number of row is ", len(dataset.index))
''''10 سطر اول داده ها'''
#print(dataset.head(10))
#dataset.info()
##################################
'''split colomns                convert dataframe to list'''
area= dataset.iloc[:,0]  ;  Area=area.tolist()
perimeter= dataset.iloc[:,1] ; Perimeter=perimeter.tolist()
major_Axis_Length= dataset.iloc[:,2] ; Major_Axis_Length=major_Axis_Length.tolist()
minor_Axis_Length= dataset.iloc[:,3] ; Minor_Axis_Length=minor_Axis_Length.tolist()
eccentricity= dataset.iloc[:,4] ; Eccentricity=eccentricity.tolist()
convex_Area= dataset.iloc[:,5] ; Convex_Area=convex_Area.tolist()
extent= dataset.iloc[:,6] ; Extent=extent.tolist()
class1=dataset.iloc[:,7] ; Class=class1.tolist()
#print(Eccentricity)
##################################
''' بیشتربن و کمترین مقدار هر ستون'''
'''''
print("min area is",min(Area))
print("min perimeter is",min(Perimeter))
print("min major axis length is",min(Major_Axis_Length))
print("min minor axis length is",min(Minor_Axis_Length))
print("min eccentricity is",min(Eccentricity))
print("min convex area is",min(Convex_Area))
print("min extent is",min(Extent))
print("max area is",max(Area))
print("max perimeter is",max(Perimeter))
print("max major axis length is",max(Major_Axis_Length))
print("max minor axis length is",max(Minor_Axis_Length))
print("max eccentricity is",max(Eccentricity))
print("max convex area is",max(Convex_Area))
print("max extent is",max(Extent))
'''
##################################
'''standard deviation'''
stdArea=np.std(Area)
stdPerimeter=np.std(Perimeter)
stdMajor=np.std(Major_Axis_Length)
stdMinor=np.std(Minor_Axis_Length)
stdEcc=np.std(Eccentricity)
stdCon=np.std(Convex_Area)
stdExtent=np.std(Extent)
#print("variance convex area is " , varCon)
########################################
''' Average'''
aveArea=np.average(Area)
avePerimeter=np.average(Perimeter)
aveMajor=np.average(Major_Axis_Length)
aveMinor=np.average(Minor_Axis_Length)
aveEcc=np.average(Eccentricity)
aveCon=np.average(Convex_Area)
aveExtent=np.average(Extent)
#print("average convex area is " , aveCon)
########################################
''' normalize function'''
def normalize(ave,std,list): # list= column in excel file
   result = []
   for x in list:
       norm= (x-ave)/std
       result.append(norm)
   return result
#########################################################
'''normalized data'''
normArea=normalize(aveArea,stdArea,Area)
normPerimeter=normalize(avePerimeter,stdPerimeter,Perimeter)
normMajor=normalize(aveMajor,stdMajor,Major_Axis_Length)
normMinor=normalize(aveMinor,stdMinor,Minor_Axis_Length)
normEcc=normalize(aveEcc,stdEcc,Eccentricity)
normCon=normalize(aveCon,stdCon,Convex_Area)
normExtent=normalize(aveExtent,stdExtent,Extent)
#print(normPerimeter)
#######################################################
''' new standard deviation     std=1 '''
stdArea1=round(np.std(normArea))
stdPerimeter1=round(np.std(normPerimeter))
stdMajor1=round(np.std(normMajor))
stdMinor1=round(np.std(normMinor))
stdEcc1=round(np.std(normEcc))
stdCon1=round(np.std(normCon))
stdExtent1=round(np.std(normExtent))
'''
print('new standard deviation is:')
print(stdExtent1)
print(stdCon1)
print(stdEcc1)
print(stdMajor1)
print(stdArea1)
print(stdMinor1)
print(stdPerimeter1)
'''
##########################################################
''' new average    ave=0'''
aveArea1=round(np.average(normArea))
avePerimeter1=round(np.average(normPerimeter))
aveMajor1=round(np.average(normMajor))
aveMinor1=round(np.average(normMinor))
aveEcc1=round(np.average(normEcc))
aveCon1=round(np.average(normCon))
aveExtent1=round(np.average(normExtent))
'''
print("######################")
print('new average is:')
print(aveExtent1)
print(aveCon1)
print(aveEcc1)
print(aveMajor1)
print(aveArea1)
print(aveMinor1)
print(avePerimeter1)
'''
#########################################
'''بخش چهارم
 ورودی داده جدید'''
ar=int(input("Area:"))        #123 234 345 456 567 678 789 :example
per= int(input("Perimeter:"))
mj=int(input("Major_Axis_Length:"))
mn= int(input("Minor_Axis_Length:"))
ecc= int(input("Eccentricity:"))
con=int(input("Convex_Area:"))
ext=int(input("Extent:"))
print(ecc)

''' نرمال سازی'''
norm0=(ar-aveArea)/stdArea
norm1=(per-aveArea)/stdPerimeter
norm2=(mj-aveArea)/stdMajor
norm3=(mn-aveArea)/stdMinor
norm4=(ecc-aveArea)/stdEcc
norm5=(con-aveArea)/stdCon
norm6=(ext-aveArea)/stdExtent
'''''
print(norm0)
print(norm1)
print(norm2)
print(norm3)
print(norm4)
print(norm5)
print(norm6)
'''
''' پیدا کردن فاصله'''
p=[norm0,norm1,norm2,norm3,norm4,norm5,norm6]
distance=[]
for i in range (len(Area)):
   q=[normArea[i] , normPerimeter[i] , normMajor[i] , normMinor[i] , normEcc[i] , normCon[i] , normExtent[i]]
   dist = math.sqrt(((p[0]-q[0]) ** 2) + ((p[1]-q[1]) ** 2) + ((p[2]-q[2]) ** 2)+ ((p[3]-q[3]) ** 2)+ ((p[4]-q[4]) ** 2)+ ((p[5]-q[5]) ** 2)+ ((p[6]-q[6]) ** 2))
   distance +=[dist]
   sortedDist=sorted(distance)
#print(distance)
#print(sortedDist)
###########################################
''' پیدا کردن kهمسایه نزدیک'''
k=20
lst=[]
for i in range(k):
   for j in range(len(distance)):
       if sortedDist[i]== distance[j]:
           lst.append(j)
#print(lst)
lstT=[] # store the type of the class for k nearst neighbor
for i in range(k):
   lstT.append(Class[lst[i]])
#print(lstT)
if lstT.count("Osmancik")<= lstT.count("Cammeo"):
   print("Cammeo is the class of the rice")
else:
   print("Osmancik is the class of the rice")
##########################################
'''بخش ششم امتیازی- نمودار'''
list=sample(Minor_Axis_Length,10)

#list=sample(normMinor,10)
print(list)
x = np.array(["A", "B", "C", "D",'E','F','G','H','I','J'])
y = np.array(list)
plt.bar(x,y)
plt.show()
