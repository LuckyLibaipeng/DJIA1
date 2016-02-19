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
%%time
DJIA['Ret_Loop']=0.0
for i in range(1,len(DJIA)):
    DJIA['Ret_Loop'][i]=np.log(DJIA['Close'][i]/DJIA['Close'][i-1])
