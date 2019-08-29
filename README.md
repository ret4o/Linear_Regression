# Linear_Regression
Working through a model for linear regression - improvements are possible. progress is negotiable.
  
    import numpy as np

    import matplotlib.pyplot as plt

    yerr=0.4
    xerr=1.3

Only use the following function if you'd like to model the data after a mathematical function. Would recommend changing the y variable and replacing plt.scatter with plt.plot on line 40ish

    def writing():
      x = np.arange(0,100,1)
      y = 4*x+np.exp(x)
      for i in range(len(x)):
          newline = str(x[i])+" "+str(y[i])+" " +str(xerr)+" "+str(yerr) 
          with open('linearfile.txt','a') as myfile:
        
              myfile.write(newline + '\n')
      myfile.close()


    ylist = []
    xlist = []

    def reading():
        myfile1=open('linearfile.txt','r')
    
        for line in myfile1:
            fields = line.split(" ")
            xlist.append(float(fields[0]))
            ylist.append(float(fields[1]))
        myfile1.close()
     return(xlist, ylist)
Above - each line is read and split into an array of 2 data points. In future I will add error bars to these lines.
#######################

    reading()
    plt.scatter(xlist,ylist)


    def calc(x,y):
        xbar = sum(x)/(len(x))
        ybar = sum(y)/(len(y))


        SSxx=0
        SSyy=0
        SPxy=0
SSxx and SSyy are the sum of squares for and y respectively. SPxy is the sum of products. xbar and ybar are the average values from the txt file.

        for ii in range(len(x)):
            SSxx+=(x[ii]-xbar)**2
            SSyy+=(y[ii]-ybar)**2
            SPxy+=(x[ii]-xbar)*(y[ii]-ybar)
        B1 = SPxy/SSxx
        B0=ybar - B1*xbar
        rline=[0.0]*len(x)
        for ii in range(len(x)):
            rline[ii] = B0+B1*float(x[ii])
        print('y = {:.2f}x+{:.2f}'.format(B1,B0))

        return(rline)


    regressionline = calc(xlist,ylist)
    plt.plot(xlist,regressionline)
    plt.xlabel('x')
    plt.ylabel('y')   
    plt.show()
    
not sure how github works. But here is calc2 - making use of SciPy package

    def calc2(x,y,input1):
    
        n=len(x)-1 #defining the limit for x 
        assert len(x)==len(y) #arrays must be equal length to fit linear rregression model
        xp = np.linspace(x[0],x[n],1000) #constructing a more defined you would like to fit to, this is what polyval does.
        p1 = scipy.polyfit(x,y,input1) #inpu1 gives the order youw
        plt.plot(xp,scipy.polyval(p1,xp)) #then in a somewhat nested fashion you use polyval on p1 (polyfit)
    
    input1 = int(input('How many orders would you like to fit for \n?'))
    calc2(x1,y1,input1)
