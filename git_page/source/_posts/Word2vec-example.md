---
title: word2vec实例
cover: /gallery/cover/dicer.png
thumbnail: /gallery/thumbnails/dicer.png
date: 2021-04-12 15:33:50
tags:
    - word2vec
categories:
    - NLP
---
## 什么是 word2vec

### one-hot

### word2vec

## 为什么是 word2vec

<!--more-->

## 自己动动手

### 爬取数据
~~~python
import requests
import random
import time
from bs4 import BeautifulSoup

def crawler():
    '''
    爬取红楼梦
    :url
    :return
    '''
    path = 'http://www.purepen.com/hlm/'
    file = open('红楼梦.txt', 'w+')
    for page in range(1, 121):
        url = path + ('000'+str(page))[-3:] + '.htm'
        print(url)
        html = requests.get(url)
        html.encoding = html.apparent_encoding
        soup = BeautifulSoup(html.text, 'lxml')
        title = soup.find(align = 'center').text
        print(title)
        content = soup.find(face = '宋体').text
        file.write(title   + '\t\n')
        file.write(content + '\t\n')
        sec = random.randint(0, 3)
        print("Sleep %d sconds." % sec)
        time.sleep(sec)

if __name__ == '__main__':
    crawler()
~~~
### 数据清洗 & 模型训练

~~~python
import re
import jieba
from gensim.models import word2vec

def segment():
    content = open('./红楼梦.txt', 'r').read()
    trimed = re.sub(r'[（）：:？“”《》，。！·、\d]+', ' ', content)
    result = ' '.join(jieba.cut(trimed))
    file = open('./cut_result.txt', 'w+')
    file.write(result)
    print("Segment Done.")

def train_model():
    sentencePath = './cut_result.txt'
    modelPath = 'hlm_model'
    sentence = word2vec.LineSentence(sentencePath)
    model = word2vec.Word2Vec(sentence, hs=1, min_count=1, window=3)
    print('Word2vec Training Done.')
    model.save(modelPath)

if __name__ == '__main__':
    segment()
    train_model()
~~~



### 模型测试

~~~ python
from gensim.models import word2vec

def analyse():
    model = word2vec.Word2Vec.load('./hlm_model')
    print('Nearest 贾宝玉:',model.wv.most_similar('贾宝玉'))
    print('Nearest 林黛玉:,',model.wv.most_similar(['林黛玉']))
    print('Nearest 薛宝钗:',model.wv.most_similar(['薛宝钗']))
    print('Nearest 晴雯:',model.wv.most_similar(['晴雯']))
    print('Nearest 袭人:',model.wv.most_similar(['袭人']))
    print('Nearest 贾母:', model.wv.most_similar(['贾母']))
    print(model.wv.doesnt_match(u"贾宝玉 薛宝钗 林黛玉 史湘云".split()))
    print(model.wv.doesnt_match(u"林黛玉 元春 探春 迎春 惜春".split()))
    print(model.wv.doesnt_match(u"贾琏 贾政 贾赦 贾敬".split()))
    print(model.wv.similarity('贾宝玉','林黛玉'))
    print(model.wv.similarity('林黛玉','薛宝钗'))
    print(model.wv.similarity('晴雯', '袭人'))

if __name__ == '__main__':
    analyse()
~~~

## References

https://blog.csdn.net/yexiaohhjk/article/details/85086503