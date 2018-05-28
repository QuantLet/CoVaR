[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **Quantile_Lasso_function** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of Quantlet:  Quantile_Lasso_function
 
Published in:      R 
  
Description:       Quantile loss function and Quantile LASSO function applying generalized approximate cross validation (GACV)
 
Keywords:          quantile_regression, loss_quantile_function, GACV, cross_validation, LASSO, 

Author:            Shih-Kang Chao
  
Submitted:         17.12.2017 by Hien Pham Thu
  


```

### R Code
```r

# library(quantreg)

loss.qr.eqn<-function(y,l_t,p){
summ<-0
for(k in 1:length(y)){
summ<-(p-as.numeric(y[k]<l_t[k]))*(y[k]-l_t[k])+summ
}
return(loss=summ)
}

GACV.qr<-function(lamb,x,y,p){
n<-length(y)
fit<-rq.fit.lasso(x,y,tau=p,lambda=lamb)
D<-0
est<-x%*%fit$coefficients
L<-loss.qr.eqn(y,est,p)
D<-length(which(abs(y[i]-est[i])<0.000001))
return(loss=L/(n-D))
}

```

automatically created on 2018-05-28