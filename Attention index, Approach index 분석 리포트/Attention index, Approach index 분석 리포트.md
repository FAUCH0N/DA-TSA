
# 연구 목적

피험자 50명의 7개 eeg 채널(FP1, FP2, F3, Fz, F4, O1, O2)과 2개의 eog채널 (vertical, horizontal) 데이터를 수집을 했다. 각 피험자가 3가지 영상(유튜브동영상, 2가지의 광고)을 시청하는 동안의 뇌파를 측정했다. 

모든 피험자가 같은 유튜브동영상 1개와 광고 2개(전기차 광고, 유니세프 광고)를 시청한다. 유튜브동영상의 길이는 약 6분정도이고 전기차 광고와 유니세프 광고는 각각 30초 가량이다. 
모든 피험자가 검은 화면 7초, 전기차광고 30초, 유튜브동영상 순서로 시청하는데, 50명 중 절반은 유니세프 광고를 유튜브동영상의 약 1분 30초 지점에서 유니세프 광고를 시청하고 나머지 절반은 유튜브동영상의 약 4분 30초 지점에서 유니세프 광고를 시청했다. 

즉, 피험자들을 두 그룹으로 나누어 중간광고 삽입 위치를 다르게 하였다. 그룹 A는 유튜브동영상의 전반부(1분 30초지점)에서 중간광고를 시청하고, 그룹 B는 유튜브동영상의 후반부(4분 30초지점)에서 중간광고를 시청했다. 

이 실험의 목적은 중간광고의 위치에 따라서 광고효과가 어떻게 변하는지 알고자 하는 것이다. 
광고효과를 피험자가 광고에 얼마나 집중하는지(집중도)와 광고에 얼마나 긍정적으로 반응했는지(동기)로 정의하고, EEG alpha파를 이용해 집중도와 동기를 측정하고자 한다. 



# 측정방법

Morgan Cerf와 Manuel Garcia-Garcia(2017)가 Consumer NeuroScience에서 제시한 방법을 따라서 집중도(Attention Index)와 동기(Approach/Withdrawal Index)를 측정했다. 

Attention Index(AI)는 한 피험자의 left frontal alpha값을 제곱한 값을 평균낸 값에 -1을 곱해서 사용한다. 

#### AI = -{(FP1 alpha)^2 + (F3 alpha)^2}/2로 정의했다. 이 AI값이 클수록 집중도가 높은 것이다.  
이 Attention Index는 사람이 무언가에 집중할때 left frontal alpha 값이 감소한다는 Klimesch(1999)와 Petersen과 Posner(2012)의 연구를 바탕으로 Morgan Cerf와 Manuel Garcia-Garcia가 제시한 측정방법이다. 

Approach/Withdrawal Index(AW)는 마찬가지로 Morgan Cerf와 Manuel Garcia-Garcia가 제시한 방법으로 좌뇌가 긍정적인 감정을 처리하고 우뇌가 부정적인 감정을 처리한다는 Coan과 Allen(2003) 그리고 Davison(2004)의 EEG frontal asymmetry theory에 기반한다. 
우뇌의 알파파 활성이 우세한 경우 Approach, 좌뇌 알파파 활성이 우세한 경우 Withdrawal로 보았다. 

#### AW = {(FP2 alhpa)^2+(F4 alpha)^2}/2 - {(FP1 alpha)^2 + (F3 alpha)^2}/2 이다. AW값이 클수록 우뇌 알파파 활성이 우세하기 때문에 Approach, AW값이 작을수록 Withdrawal 동기를 가졌다고 할 수 있다. 



# 데이터 설명

각 피험자의 원본 뇌파데이터에서 linefrequncy(60Hz)와 EOG artifact를 제거, alpha band를 추출하고, 영상을 시청한 부분의 뇌파만 잘라낸 데이터를 사용한다. 이 분석에서는 각 피험자의 뇌파데이터에서 AI와 AW값을 계산하고 표준화한 뒤에 A그룹끼리, B그룹끼리 평균낸 값을 A그룹의 AI, AW, B그룹의 AI, BW로 한다. 이 분석에 사용된 데이터는 미리 linefrequncy(60Hz)와 EOG artifact를 제거하고 alpha band만 추출한 데이터이다. 




# 분석절차

이 분석에서는 50명 각 피험자의 뇌파데이터에서 AI와 AW값을 계산하고 표준화한 뒤에 A그룹끼리, B그룹끼리 평균낸 값을 A그룹의 AI, AW, B그룹의 AI, BW로 한다.
1. 50명 각 피험자의 AI, AW계산 후, 50명을 A그룹, B그룹으로 나누어 각 그룹의 AI, AW의 평균값 계산
3. 시계열 시각화
 



# 분석

## 1. 각 피험자의 AI, AW계산


```python
import pandas as pd 
import numpy as np 
from scipy import stats
import glob
```


```python
#처리할 파일 목록
als = sorted(glob.glob("*A.xlsx")) #그룹 A: 중간광고 삽입위치가 영상의 전반부인 그룹의 피험자리스트
bls =sorted(glob.glob("*B.xlsx")) #그룹 B: 중간광고 삽입위치가 영상의 후반부인 그룹의 피험자리스트 
print(als, bls)
print(len(als),len(bls))
```

    ['101A.xlsx', '103A.xlsx', '105A.xlsx', '107A.xlsx', '109A.xlsx', '111A.xlsx', '113A.xlsx', '115A.xlsx', '117A.xlsx', '119A.xlsx', '121A.xlsx', '123A.xlsx', '125A.xlsx', '127A.xlsx', '129A.xlsx', '131A.xlsx', '133A.xlsx', '135A.xlsx', '137A.xlsx', '139A.xlsx', '141A.xlsx', '143A.xlsx', '145A.xlsx', '147A.xlsx', '149A.xlsx'] ['102B.xlsx', '104B.xlsx', '106B.xlsx', '108B.xlsx', '110B.xlsx', '112B.xlsx', '114B.xlsx', '116B.xlsx', '118B.xlsx', '120B.xlsx', '122B.xlsx', '124B.xlsx', '126B.xlsx', '128B.xlsx', '130B.xlsx', '132B.xlsx', '134B.xlsx', '136B.xlsx', '138B.xlsx', '140B.xlsx', '142B.xlsx', '144B.xlsx', '146B.xlsx', '148B.xlsx', '150B.xlsx']
    25 25



```python
pd.read_excel(als[0]).head() #피험자 번호 101A의 뇌파데이터 확인
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fp1_alpha</th>
      <th>fp2_alpha</th>
      <th>f3_alpha</th>
      <th>fz_alpha</th>
      <th>f4_alpha</th>
      <th>o1_alpha</th>
      <th>o2_alpha</th>
      <th>fp1_alpha_zscore</th>
      <th>fp2_alpha_zscore</th>
      <th>o1_alpha_zscore</th>
      <th>o2_alpha_zscore</th>
      <th>AttentionIndex</th>
      <th>AWIndex</th>
      <th>index</th>
      <th>f3_alpha_zscore</th>
      <th>fz_alpha_zscore</th>
      <th>f4_alpha_zscore</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.005854</td>
      <td>-0.000661</td>
      <td>0.004380</td>
      <td>0.002075</td>
      <td>-0.002879</td>
      <td>-0.003361</td>
      <td>-0.004695</td>
      <td>4.537927</td>
      <td>-1.019698</td>
      <td>-2.025072</td>
      <td>-3.367858</td>
      <td>-8.951061</td>
      <td>-8.372378</td>
      <td>0</td>
      <td>4.482361</td>
      <td>2.470089</td>
      <td>-2.979048</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.005891</td>
      <td>-0.000664</td>
      <td>0.004322</td>
      <td>0.002041</td>
      <td>-0.002909</td>
      <td>-0.003245</td>
      <td>-0.004684</td>
      <td>4.566658</td>
      <td>-1.024628</td>
      <td>-1.955129</td>
      <td>-3.359802</td>
      <td>-8.967878</td>
      <td>-8.483124</td>
      <td>1</td>
      <td>4.422921</td>
      <td>2.429718</td>
      <td>-3.010387</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.005905</td>
      <td>-0.000676</td>
      <td>0.004229</td>
      <td>0.001992</td>
      <td>-0.002919</td>
      <td>-0.003127</td>
      <td>-0.004656</td>
      <td>4.577620</td>
      <td>-1.042487</td>
      <td>-1.883938</td>
      <td>-3.340376</td>
      <td>-8.883286</td>
      <td>-8.521991</td>
      <td>2</td>
      <td>4.328061</td>
      <td>2.371943</td>
      <td>-3.021088</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.005898</td>
      <td>-0.000693</td>
      <td>0.004105</td>
      <td>0.001932</td>
      <td>-0.002908</td>
      <td>-0.003008</td>
      <td>-0.004609</td>
      <td>4.572705</td>
      <td>-1.068252</td>
      <td>-1.812120</td>
      <td>-3.306652</td>
      <td>-8.706450</td>
      <td>-8.496888</td>
      <td>3</td>
      <td>4.201270</td>
      <td>2.299643</td>
      <td>-3.009497</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.005872</td>
      <td>-0.000712</td>
      <td>0.003953</td>
      <td>0.001860</td>
      <td>-0.002875</td>
      <td>-0.002889</td>
      <td>-0.004540</td>
      <td>4.552106</td>
      <td>-1.098468</td>
      <td>-1.740845</td>
      <td>-3.256679</td>
      <td>-8.444545</td>
      <td>-8.409456</td>
      <td>4</td>
      <td>4.045199</td>
      <td>2.214224</td>
      <td>-2.975705</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.read_excel(bls[0]).head() #피험자 번호 102B의 뇌파데이터 확인
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fp1_alpha</th>
      <th>fp2_alpha</th>
      <th>f3_alpha</th>
      <th>fz_alpha</th>
      <th>f4_alpha</th>
      <th>o1_alpha</th>
      <th>o2_alpha</th>
      <th>fp1_alpha_zscore</th>
      <th>fp2_alpha_zscore</th>
      <th>o1_alpha_zscore</th>
      <th>o2_alpha_zscore</th>
      <th>AttentionIndex</th>
      <th>AWIndex</th>
      <th>index</th>
      <th>f3_alpha_zscore</th>
      <th>fz_alpha_zscore</th>
      <th>f4_alpha_zscore</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.003611</td>
      <td>-0.001882</td>
      <td>-0.001583</td>
      <td>-0.000884</td>
      <td>0.000237</td>
      <td>0.003570</td>
      <td>0.004014</td>
      <td>-2.390299</td>
      <td>-1.203740</td>
      <td>1.957080</td>
      <td>2.231422</td>
      <td>-0.460901</td>
      <td>-1.056703</td>
      <td>0</td>
      <td>-1.715499</td>
      <td>-1.049624</td>
      <td>0.236933</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.003439</td>
      <td>-0.001783</td>
      <td>-0.001558</td>
      <td>-0.000867</td>
      <td>0.000170</td>
      <td>0.003554</td>
      <td>0.003998</td>
      <td>-2.276609</td>
      <td>-1.140341</td>
      <td>1.948047</td>
      <td>2.222323</td>
      <td>-0.399266</td>
      <td>-0.963963</td>
      <td>1</td>
      <td>-1.688470</td>
      <td>-1.029503</td>
      <td>0.169521</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.003270</td>
      <td>-0.001689</td>
      <td>-0.001535</td>
      <td>-0.000852</td>
      <td>0.000098</td>
      <td>0.003523</td>
      <td>0.003964</td>
      <td>-2.164699</td>
      <td>-1.080268</td>
      <td>1.931351</td>
      <td>2.203890</td>
      <td>-0.342348</td>
      <td>-0.875534</td>
      <td>2</td>
      <td>-1.663326</td>
      <td>-1.011669</td>
      <td>0.097716</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.003100</td>
      <td>-0.001596</td>
      <td>-0.001509</td>
      <td>-0.000835</td>
      <td>0.000026</td>
      <td>0.003482</td>
      <td>0.003919</td>
      <td>-2.052220</td>
      <td>-1.020803</td>
      <td>1.908506</td>
      <td>2.178465</td>
      <td>-0.288203</td>
      <td>-0.790514</td>
      <td>3</td>
      <td>-1.635159</td>
      <td>-0.991052</td>
      <td>0.026532</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.002928</td>
      <td>-0.001500</td>
      <td>-0.001476</td>
      <td>-0.000811</td>
      <td>-0.000040</td>
      <td>0.003431</td>
      <td>0.003864</td>
      <td>-1.937762</td>
      <td>-0.959803</td>
      <td>1.880734</td>
      <td>2.147893</td>
      <td>-0.235574</td>
      <td>-0.708793</td>
      <td>4</td>
      <td>-1.599654</td>
      <td>-0.963541</td>
      <td>-0.039252</td>
    </tr>
  </tbody>
</table>
</div>




```python
#그룹 A 각 피험자의 AI와 AW계산 (비교를 위해 다른 인덱스도 함께 계산)
AI = pd.DataFrame()
AW = pd.DataFrame()


for data in als: 
    
    df=pd.read_excel(data)
    
    #각 피험자의 인덱스들 계산 
    df['AI']=-(df.fp1_alpha**2+df.f3_alpha**2)/2
    df['AW']=(df.fp2_alpha**2+df.f4_alpha**2)/2-(df.fp1_alpha**2+df.f3_alpha**2)/2

                           
    #그룹 A 25명의 각각의 인덱스들을 표준화하여 하나의 변수에 저장함                    
    AI = pd.concat([AI, pd.DataFrame(stats.zscore(df['AI']))], axis =1, ignore_index=True)
    AW = pd.concat([AW, pd.DataFrame(stats.zscore(df['AW']))], axis =1, ignore_index=True)
            
    


```


```python
AI.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>15</th>
      <th>16</th>
      <th>17</th>
      <th>18</th>
      <th>19</th>
      <th>20</th>
      <th>21</th>
      <th>22</th>
      <th>23</th>
      <th>24</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-9.609840</td>
      <td>0.031212</td>
      <td>-4.878892</td>
      <td>0.382385</td>
      <td>0.233767</td>
      <td>0.132473</td>
      <td>0.093371</td>
      <td>-0.012943</td>
      <td>-0.353900</td>
      <td>0.231363</td>
      <td>...</td>
      <td>0.167561</td>
      <td>0.346835</td>
      <td>0.207575</td>
      <td>0.212578</td>
      <td>0.425133</td>
      <td>0.208903</td>
      <td>0.182827</td>
      <td>0.405019</td>
      <td>0.235505</td>
      <td>0.363115</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-9.596578</td>
      <td>0.035303</td>
      <td>-4.833896</td>
      <td>0.385021</td>
      <td>0.224891</td>
      <td>0.136574</td>
      <td>0.104696</td>
      <td>-0.040665</td>
      <td>-0.391599</td>
      <td>0.244847</td>
      <td>...</td>
      <td>0.173903</td>
      <td>0.344960</td>
      <td>0.221639</td>
      <td>0.207013</td>
      <td>0.386993</td>
      <td>0.210116</td>
      <td>0.298614</td>
      <td>0.402085</td>
      <td>0.260716</td>
      <td>0.357004</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-9.478264</td>
      <td>0.038484</td>
      <td>-4.772277</td>
      <td>0.383315</td>
      <td>0.221012</td>
      <td>0.138961</td>
      <td>0.116128</td>
      <td>-0.066613</td>
      <td>-0.404878</td>
      <td>0.279736</td>
      <td>...</td>
      <td>0.176806</td>
      <td>0.344598</td>
      <td>0.237239</td>
      <td>0.202089</td>
      <td>0.330610</td>
      <td>0.212065</td>
      <td>0.366730</td>
      <td>0.399493</td>
      <td>0.282330</td>
      <td>0.350022</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-9.268902</td>
      <td>0.040671</td>
      <td>-4.694851</td>
      <td>0.380069</td>
      <td>0.223560</td>
      <td>0.139244</td>
      <td>0.126663</td>
      <td>-0.088941</td>
      <td>-0.405603</td>
      <td>0.319593</td>
      <td>...</td>
      <td>0.176878</td>
      <td>0.344007</td>
      <td>0.254858</td>
      <td>0.197957</td>
      <td>0.266729</td>
      <td>0.214628</td>
      <td>0.384951</td>
      <td>0.397250</td>
      <td>0.299972</td>
      <td>0.342339</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-8.977449</td>
      <td>0.041843</td>
      <td>-4.601783</td>
      <td>0.377134</td>
      <td>0.230882</td>
      <td>0.137447</td>
      <td>0.135874</td>
      <td>-0.105623</td>
      <td>-0.396351</td>
      <td>0.359977</td>
      <td>...</td>
      <td>0.176232</td>
      <td>0.342648</td>
      <td>0.274241</td>
      <td>0.194746</td>
      <td>0.206306</td>
      <td>0.217742</td>
      <td>0.357288</td>
      <td>0.395232</td>
      <td>0.313423</td>
      <td>0.334217</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 25 columns</p>
</div>




```python
Ares=pd.DataFrame()

Ares['AI']=AI.mean(axis=1)
Ares['AW']=AW.mean(axis=1)


Ares.to_excel('Group A 인덱스.xlsx')

```


```python
Ares.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AI</th>
      <th>AW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.396279</td>
      <td>-0.526412</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.390465</td>
      <td>-0.514844</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.381795</td>
      <td>-0.501314</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.371358</td>
      <td>-0.487887</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.358849</td>
      <td>-0.474059</td>
    </tr>
  </tbody>
</table>
</div>




```python
#그룹 B 각피험자의 AI와 AW계산 (비교를 위해 다른 인덱스도 함께 계산)

B_AI = pd.DataFrame()
B_AW = pd.DataFrame()


for data in bls: 
    
    df=pd.read_excel(data)
    
    #각 피험자의 인덱스들 계산
    df['AI']=-(df.fp1_alpha**2+df.f3_alpha**2)/2
    df['AW']=(df.fp2_alpha**2+df.f4_alpha**2)/2-(df.fp1_alpha**2+df.f3_alpha**2)/2
    
    #그룹 B 25명의 각각의 인덱스들을 표준화하여 하나의 변수에 저장함                    
    B_AI = pd.concat([B_AI, pd.DataFrame(stats.zscore(df['AI']))], axis =1, ignore_index=True)
    B_AW = pd.concat([B_AW, pd.DataFrame(stats.zscore(df['AW']))], axis =1, ignore_index=True)

                      


```


```python
Bres=pd.DataFrame()

Bres['AI']=B_AI.mean(axis=1)
Bres['AW']=B_AW.mean(axis=1)

Bres.to_excel('Group B 인덱스.xlsx')


```


```python
Bres.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AI</th>
      <th>AW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.081617</td>
      <td>-0.084125</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.083184</td>
      <td>-0.084155</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.087361</td>
      <td>-0.084536</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.093719</td>
      <td>-0.085576</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.101525</td>
      <td>-0.087926</td>
    </tr>
  </tbody>
</table>
</div>




```python
df=pd.concat([Ares,Bres])
df.to_excel('Group AB index.xlsx')
```

## 1. Attention index

Morgan Cerf와 Manuel Garcia-Garcia(2017)가 Consumer NeuroScience에서 제시한 방법을 따라서 집중도(Attention Index)와 동기(Approach/Withdrawal Index)를 측정했다. 

Attention Index(AI)는 한 피험자의 left frontal alpha값을 제곱한 값을 평균낸 값에 -1을 곱해서 사용한다. 

#### AI = -{(FP1 alpha)^2 + (F3 alpha)^2}/2로 정의했다. 이 AI값이 클수록 집중도가 높은 것이다.  
이 Attention Index는 사람이 무언가에 집중할때 left frontal alpha 값이 감소한다는 Klimesch(1999)와 Petersen과 Posner(2012)의 연구를 바탕으로 Morgan Cerf와 Manuel Garcia-Garcia가 제시한 측정방법이다. 


```python
df=pd.read_excel('Group AB index.xlsx')
```


```python
df['group']=np.where(df.index<len(Ares),'A','B');df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>AI</th>
      <th>AW</th>
      <th>group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>-0.396279</td>
      <td>-0.526412</td>
      <td>A</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>-0.390465</td>
      <td>-0.514844</td>
      <td>A</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>-0.381795</td>
      <td>-0.501314</td>
      <td>A</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>-0.371358</td>
      <td>-0.487887</td>
      <td>A</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>-0.358849</td>
      <td>-0.474059</td>
      <td>A</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['time']=df.iloc[:,0:1]
idx=df.pivot(index='time', columns='group', values='AI')
```


```python
idx.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>group</th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>time</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.396279</td>
      <td>-0.081617</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.390465</td>
      <td>-0.083184</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.381795</td>
      <td>-0.087361</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.371358</td>
      <td>-0.093719</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.358849</td>
      <td>-0.101525</td>
    </tr>
  </tbody>
</table>
</div>




```python
import matplotlib.pyplot as plt
result = pd.DataFrame({
                      'Group A': idx.A,
                       'Group B':idx.B})
sns.set_style("white")
result.plot(title="Attention: Group A vs B")
plt.gcf().set_size_inches(12,8)
```


![png](output_28_0.png)


#### 그룹 A, B간의 Attention Index 차이를 비교하기 위해서 단순이동평균을 적용한 결과이다. 1만개 데이터 (10초)로 이동평균 구했다
그 결과 중간광고가 삽입된 시점에서 Attention이 크게 낮아진 것을 확인할 수 있다. 

그래프에서 회색으로 표시된 부분은 A그룹이 중간광고를 시청하는 시간이고, 빨간색으로 표시된 부분은 B그룹이 중간광고를 시청하는 부분이다.


```python
ra = idx.A.rolling(10000).mean()
rb = idx.B.rolling(10000).mean()

result = pd.DataFrame({
                      '10000_MA_Group A': ra,
                       '10000_MA_Group B:':rb})



result.plot(title="Attention: Group A vs B")

plt.gcf().set_size_inches(12,8)
plt.axvspan(131000, 161000, color='gray', alpha=0.1)
plt.axvspan(319000, 349000, color='red', alpha=0.1)
plt.show()
```


![png](output_30_0.png)


두 그룹의 중간광고 부분만 비교하면 다음과 같다


```python
ra = idx.A.rolling(10000).mean()
rb = idx.B.rolling(10000).mean()

result = pd.DataFrame({
                      '10000_MA_Group A': ra[131000:161000].reset_index(drop=True),
                       '10000_MA_Group B:':rb[319000:349000].reset_index(drop=True)})


sns.set_style("white")
plt.show()
result.plot(title="Attention: Group A vs B")

plt.gcf().set_size_inches(12,8)
plt.show()
```


![png](output_32_0.png)


### 중간광고 앞에 본 영상이 중간광고를 시청하는데 영향을 주지 않고 중간광고 시작 이후에는  Attention level이 중간광고에 의해서만 변한다고 가정하면, 두 그래프를 시작점을 같게 평행이동한 후 비교할 수 있다.

## 두 그래프의 시작점을 같게하고 비교한 결과 0초에서 6초 사이(빨간색으로 표시된 부분)의 A,B그룹간의 Attention의 차이가 있는 것으로 보인다.


```python
result = pd.DataFrame({
                      '10000_MA_Group A': ra[131000:161000].reset_index(drop=True)-ra[131000:131001].values,
                       '10000_MA_Group B:':rb[319000:349000].reset_index(drop=True)-rb[319000:319001].values})


result.plot(title="Attention: Group A vs B")

plt.gcf().set_size_inches(12,8)
plt.axvspan(0, 6000, color='red', alpha=0.1)
plt.show()
```


![png](output_34_0.png)


## 0초에서 6초 사이에서 그룹 B의 평균 attention level이 그룹 A보다 높을 것이다는 가설검정을 한다.


```python
x=pd.DataFrame()
x['A']=(ra[131000:137000].reset_index(drop=True)-ra[131000:131001].values)
x['B']=(rb[319000:325000].reset_index(drop=True)-rb[319000:319001].values)
```


```python
x.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6000.000000</td>
      <td>6000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-0.015680</td>
      <td>-0.004577</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.014893</td>
      <td>0.006663</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-0.039825</td>
      <td>-0.019392</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-0.031870</td>
      <td>-0.009816</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-0.011396</td>
      <td>-0.003365</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>-0.001353</td>
      <td>0.000058</td>
    </tr>
    <tr>
      <th>max</th>
      <td>0.004335</td>
      <td>0.009420</td>
    </tr>
  </tbody>
</table>
</div>




```python
#정규성과 등분산 가정 t-test
from scipy.stats import ttest_ind

stat, p = ttest_ind(x.A, x.B)
print ('t-stats = ',stat)
print('p-value =  ',p)
```

    t-stats =  -52.71555210606807
    p-value =   0.0


### 정규성과 등분산성을 가정했을때 t-test 결과 t=-52.7, p<.000으로 두 그룹간의 차이는 통계적으로 유의하다


```python
#정규성 검정 Shapiro-Wilk Test
from scipy.stats import shapiro
stat, p = shapiro(x.A)
print ('stat:   ',stat)
print('p-value:',p)
```

    stat:    0.884483814239502
    p-value: 0.0



```python
#정규성 검정 Shapiro-Wilk Test
from scipy.stats import shapiro
stat, p = shapiro(x.B)
print ('stat:   ',stat)
print('p-value:',p)
```

    stat:    0.9784667491912842
    p-value: 3.342883248088766e-29


### 정규성 검정 결과 p<0.000으로 두 표본이 모두 정규성을 만족하지 않으므로 Wilcoxon Sign-Ranked test를 진행한다


```python
x['difference'] = x['B'] - x['A']
x['difference'][x['difference']==0]
```




    0    0.0
    Name: difference, dtype: float64




```python
stats.wilcoxon(x['difference'])
```




    WilcoxonResult(statistic=4003826.0, pvalue=2.014799647594513e-303)



### Wilcoxon Sign-Ranked Test 결과 t=4003826.0, p<0.000으로 B그룹의 median이 A그룹의 median보다 높은 것으로 나타났다.

##  Attention index 분석결과 요약
Wilcoxon Sign-Ranked Test 결과 t=4003826.0, p<0.000으로 B그룹의 median이 A그룹의 median보다 높은 것으로 나타났다. 따라서 3초에서 6초 사이에서 그룹 B의 attention level이 그룹 A보다 높다.

### 즉, 중간광고 삽입위치가 전반부일때 보다 후반부일때 0초부터 6초사이의 attention이 더 높았다


```python
result = pd.DataFrame({
                      '10000_MA_Group A': ra[131000:137000].reset_index(drop=True)-ra[131000:131001].values,
                       '10000_MA_Group B:':rb[319000:325000].reset_index(drop=True)-rb[319000:319001].values})


result.plot(title="Attention: Group A vs B")

plt.gcf().set_size_inches(12,8)
#plt.axvspan(0, 6000, color='red', alpha=0.1)
plt.show()
```


![png](output_47_0.png)


## 2. Approach index
