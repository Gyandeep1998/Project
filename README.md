# Project
#State Independent Balking RBOS probability
from operator import truediv
def p_0(lmd,mu,nu,p):
    lst_1=[]
    lst_2=[]
    newlst=[1]
    prod=1
    for k in range (1,30):
        num=(lmd**k)*(1-p)**(k-1)#Numerator part of p_0
        lst_1.append(num)
        for j in range (1,k+1):
            den_0=mu+(j-1)*nu #denominator part of p_0
            prod=den_0*prod
        lst_2.append(prod) #It contains the product of elements from den_0 along with previous term products
    newlst.extend(lst_2) # It contains the same elemets with additional term 1 
    newlst.pop(-1)       #Last term is removed from newlst
    den=list(map(truediv,lst_2,newlst)) #Dividing lst_2 by newlst to get product of k terms given by p_0 
    ad=list(map(truediv,lst_1,den))     #Dividing lst_1 by den to get right part of p_0
    rslt=(1+sum(ad))**(-1)
    return rslt
    
    
   #Calculation of p_n 
    def p_n(lmd,mu,nu,n,p):
    lst_11=[]
    pro=1
    num_1=(lmd**n)*(1-p)**(n-1)
    for j in range (1,n+1):
        den_01=mu+(j-1)*nu
        lst_11.append(den_01)
        for num in lst_11:
            pro=pro*num
    rslt=num_1/pro
    return rslt*p_0(lmd,mu,nu,p)
