# COVID-19 전망
COVID-19 전망
kaggle에서 코로나 현황을 다운 받아 최근 데이터를 추가하여 csv파일로 만들어서 이전 자료를 분석한다.

import csv


stdate = ''  # 팬터믹이 시작된 날짜
eddate = ''  # 팬더믹이 종료된 날짜 
days   = 0   # 펜더믹은 5일이상 100일 이상인 날짜 (시작기준), 펜더믹 종료는 펜더믹 시작 후 5일동안 단 한번도 100명이 증가되지 않는 마지막 100 일 이상일자 


f = open ('covid_19_data_new.csv', encoding="cp949")
data = csv.reader(f) 
next(data)

# 펜더믹의 시작일 찾기 
for row in data :
    if row[4] == '' :
        row[4] = 0
         row[4] = float(row[4])
    
    if days == 5 : 
        break
    else : 
        if row[4] >= 100 :  
            if stdate == '' :
                stdate = row[0] 
            
            days = days + 1
        else :
            if days > 0 :
                stdate = ''
                days = 0

print ("펜데믹 시작일 : %s"%stdate)        

# 펜데믹 종료일 찾기 
days = 0
if stdate  != '' :
    for row in data :
        if row[0] <= stdate :
            continue
       row[4] = float(row[4])
        if row[4] >= 100 :
            days = 0
            eddate = ''
        else :
            if eddate == '':
                eddate = row[0]
                
            days = days + 1
        
        if days == 5 : 
            break
            
    print("펜데믹 종료일 : %s"%eddate)
        
        
        
    
펜데믹 시작일 : 2020-02-20
펜데믹 종료일 : 2020-04-01
 
