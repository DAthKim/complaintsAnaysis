# complaintsAnaysis
Analysis of complaints
- personal information issue to upload
- using amounts of 48 files 
# Description
- complaints analysis is displayed by wordcloud
- 11 parts is here
- make wordcloud by quater, parts(question, request, suggest)
# Characteristic
- wordcloud by python
- language : python
- tool : Google colab
# Quick view
```
pip install konlpy
```
```
import pandas as pd
import numpy as np
from konlpy.tag import Okt
from wordcloud import WordCloud, ImageColorGenerator, STOPWORDS
import matplotlib.pyplot as plt
%matplotlib inline
okt = Okt()
import matplotlib.font_manager as fm
import re
from PIL import Image
from io import BytesIO 
import datetime
from collections import Counter
```
```
labels = ['place','date','messenger','category','type','due','summary','name','phone','email','detail','receive','address','end','period','address_detail','result','result_detail','sign','etc']
data_arp = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/sounds/sounds_place_arparking.csv', names = labels, encoding='cp949')
data_arp.head()
```
```
circle_mask = np.array(Image.open('/content/drive/MyDrive/Colab Notebooks/circle_img.jpg'))
```
```
arp_detail = data_arp['detail']
arp_d_tolist = arp_detail.values.tolist()
arp_d_list = ''
for i in arp_d_tolist:
  arp_d_list += i
arp_d_nouns = okt.nouns(arp_d_list)
arp_d_n = ''
for i in arp_d_nouns:
  arp_d_n += i+' '
arp_d_nouns_count = Counter(arp_d_nouns)
stopwords = set(STOPWORDS)
stopwords.update(['주차장','아름동'])
```
```
wd_arp_d = WordCloud(max_font_size=200,background_color="white",mask=circle_mask,font_path='/content/drive/MyDrive/Colab Notebooks/sounds/malgun.ttf',stopwords=stopwords).generate(arp_d_n)
fig = plt.figure()
plt.imshow(wd_arp_d, interpolation='bilinear')
plt.axis('off')
wd_arp_d.to_file(filename='/content/drive/MyDrive/Colab Notebooks/wordcloud_img/wd_arp_d.jpg')
```
```
arp_question = data_arp[data_arp['type'] == "질의"]
arp_question_detail = arp_question['detail']

arp_check = data_arp[data_arp['type'] == "확인"]
arp_check_detail = arp_check['detail']

arp_request = data_arp[data_arp['type'] == "건의"]
arp_request_detail = arp_request['detail']
```
질의
```
arp_qd_tolist = arp_question_detail.values.tolist()
arp_qd_list = ''
for i in arp_qd_tolist:
  arp_qd_list += i
```
```
arp_qd_nouns = okt.nouns(arp_qd_list)
arp_qd_n = ''
for i in arp_qd_nouns:
  arp_qd_n += i+' '
```
```
arp_qd_nouns_count = Counter(arp_qd_nouns)
arp_qd_nouns_count
```
```
stopwords = set(STOPWORDS)
# stopwords.update(['모집', '임대', '아파트', '행복'])
```
```
wd_arp_qd = WordCloud(max_font_size=250,background_color="white",mask=circle_mask,font_path='/content/drive/MyDrive/Colab Notebooks/sounds/malgun.ttf',stopwords=stopwords).generate(arp_qd_n)
fig = plt.figure()
plt.imshow(wd_arp_qd, interpolation='bilinear')
plt.axis('off')
wd_arp_qd.to_file(filename='/content/drive/MyDrive/Colab Notebooks/wordcloud_img/wd_arp_qd.jpg')
```

확인
```
arp_cd_tolist = arp_check_detail.values.tolist()
arp_cd_list = ''
for i in arp_cd_tolist:
  arp_cd_list += i
```
```
arp_cd_nouns = okt.nouns(arp_cd_list)
arp_cd_n = ''
for i in arp_cd_nouns:
  arp_cd_n += i+' '
```
```
arp_cd_nouns_count = Counter(arp_cd_nouns)
arp_cd_nouns_count
```
```
stopwords = set(STOPWORDS)
# stopwords.update(['모집', '임대', '아파트', '행복'])
```
```
wd_arp_cd = WordCloud(max_font_size=300,background_color="white",mask=circle_mask,font_path='/content/drive/MyDrive/Colab Notebooks/sounds/malgun.ttf',stopwords=stopwords).generate(arp_cd_n)
fig = plt.figure()
plt.imshow(wd_arp_cd, interpolation='bilinear')
plt.axis('off')
wd_arp_cd.to_file(filename='/content/drive/MyDrive/Colab Notebooks/wordcloud_img/wd_arp_cd.jpg')
```
건의
```
arp_rd_tolist = arp_request_detail.values.tolist()
arp_rd_list = ''
for i in arp_rd_tolist:
  arp_rd_list += i
```
```
arp_rd_nouns = okt.nouns(arp_rd_list)
arp_rd_n = ''
for i in arp_rd_nouns:
  arp_rd_n += i+' '
```
```
arp_rd_nouns_count = Counter(arp_rd_nouns)
arp_rd_nouns_count
```
```
stopwords = set(STOPWORDS)
stopwords.update(['주차장','아름동'])
```
```
wd_arp_rd = WordCloud(max_font_size=250,background_color="white",mask=circle_mask,font_path='/content/drive/MyDrive/Colab Notebooks/sounds/malgun.ttf',stopwords=stopwords).generate(arp_rd_n)
fig = plt.figure()
plt.imshow(wd_arp_rd, interpolation='bilinear')
plt.axis('off')
wd_arp_rd.to_file(filename='/content/drive/MyDrive/Colab Notebooks/wordcloud_img/wd_arp_rd.jpg')
```
