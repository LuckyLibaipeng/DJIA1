# -*- coding: utf-8 -*-
"""
Created on Fri Feb 19 21:15:21 2016

@author: Administrator
"""

import pandas.io.data as web
DJIA=web.DataReader(name='DJIA',data_source='yahoo',start='2000-1-1')
DJIA.info()
DJIA.tail()
DJIA['Close'].plot(figsize=(8,5))
import matplotlib.pyplot as plt
plt.show()
#DJIA指数历史水平
import numpy as np
#计算单个对数收益率值
%time
DJIA['Ret_Loop']=0.0
for i in range(1,len(DJIA)):
    DJIA['Ret_Loop'][i]=np.log(DJIA['Close'][i]/DJIA['Close'][i-1])
DJIA[['Close','Ret_Loop']].tail()
#一个索引位置
%time DJIA['Return']=np.log(DJIA['Close']/DJIA['Close'].shift(1))
DJIA[['Close','Ret_Loop','Return']].tail()
del DJIA['Ret_Loop']
DJIA[['Close','Return']].plot(subplots=True,style='b',figsize=(8,5))
plt.show()
#移动平均值
import pandas as pd
DJIA['42d']=pd.rolling_mean(DJIA['Close'],window=42)
DJIA['252d']=pd.rolling_mean(DJIA['Close'],window=252)
DJIA[['Close','42d','252d']].tail()
DJIA[['Close','42d','252d']].plot(figsize=(8,5))
#移动历史波动率,杠杆效应
import math
DJIA['Mov_Vol']=pd.rolling_std(DJIA['Return'],window=252)*math.sqrt(252)#moving annual volatility
DJIA[['Close','Mov_Vol','Return']].plot(subplots=True,style='b',figsize=(8,7))
