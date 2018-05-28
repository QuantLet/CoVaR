[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **ConfidenceBand_Plot** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of Quantlet:  ConfidenceBand_Plot
 
Published in:      R 
  
Description:       Create scatterplot with asymptotic and bootstrap confidence bands as well as linear regression and quantile regression
 
Keywords:          confidence_band, bootstrap, quantile_regression, asymptotic_confidence band, plot, linear_regression

Author:            Shih-Kang Chao, Hien Pham Thu
  
Submitted:         15.12.2017 by Hien Pham Thu
  


```

### R Code
```r

#### PLOT Confidence Band ####
##############################
library(quantreg)
library(KernSmooth)
library(foreign)

#########################################################
source("ConfidenceBand.r")
############## Data with BOA and Citi ###################
MarketData_FULL = read.table("MarketData_CDS-G14.txt")
CDS_FULL = read.table("CDS_G14.txt")

Y_CDS_Var1 = CDS_FULL[,10] # daily CDS spread returns
X_Market_Var1 = MarketData_FULL[,2] # citi

Y_CDS_Var2 = CDS_PRE[,10] # daily CDS spread returns
X_Market_Var2 = MarketData_PRE[,2] # citi

############## Confidence Band ###########################

fit1<-conf(X_Market_Var1, Y_CDS_Var1, q = 0.01, gridn = 100, alpha=0.05, B=100)

fit2<-conf(X_Market_Var2, Y_CDS_Var2, q = 0.01, gridn = 100, alpha=0.05, B=100)


############## Plot ######################################
par(mfcol=c(1,2)) # For multiple figures

#############   FIGURE 1  ################################
plot(X_Market_Var1, Y_CDS_Var1,pch=20,cex=1.2, xlab="State Variables Returns",ylab="CDS Spreads Returns",cex.axis=1.2, cex.lab=1.3, lab = c(3,3,0), ylim = c(min(Y_CDS_Var1)-0.2,max(Y_CDS_Var1)+0.10),main="") #Returns scatter plot and Quantile Function
abline(para<-rq(Y_CDS_Var1 ~ (X_Market_Var1), tau = 0.01) , col = "red", lty = 1, lwd=3) # linear quantile function
lines(fit1$x0, fit1$est, col = "blue2", lwd=3)
lines(fit1$x0, fit1$asy.l,col = "magenta", lty = 2, lwd=4)
lines(fit1$x0, fit1$asy.h,col = "magenta", lty = 2, lwd=4)
lines(fit1$x0, fit1$boot.l,col = "red", lty = 4, lwd=4)
lines(fit1$x0, fit1$boot.h,col = "red", lty = 4, lwd=4)


#############   FIGURE 2  #################################
plot(X_Market_Var2, Y_CDS_Var2,pch=20,cex=1.2, xlab="State Variables Returns",ylab="CDS Spreads Returns",cex.axis=1.2, cex.lab=1.3, lab = c(3,3,0), ylim = c(min(Y_CDS_Var2)-0.2,max(Y_CDS_Var2)+0.10),main="") #Returns scatter plot and Quantile Function
abline(para<-rq(Y_CDS_Var2 ~ (X_Market_Var2), tau = 0.01) , col = "red", lty = 1, lwd=3) # linear quantile function
lines(fit2$x0, fit2$est, col = "blue2", lwd=3)
lines(fit2$x0, fit2$asy.l,col = "magenta", lty = 2, lwd=4)
lines(fit2$x0, fit2$asy.h,col = "magenta", lty = 2, lwd=4)
lines(fit2$x0, fit2$boot.l,col = "red", lty = 4, lwd=4)
lines(fit2$x0, fit2$boot.h,col = "red", lty = 4, lwd=4)

```

automatically created on 2018-05-28