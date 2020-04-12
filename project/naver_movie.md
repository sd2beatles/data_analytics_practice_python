```python

BASEURL='https://openapi.naver.com/v1/search/movie.json?query=%s'
DISPLAY=BASEURL+'&display=%s'
START=DISPLAY+'&start=%s'

client_id='mGheSDZSqWyhMF5gFAqU'
client_secret='i3HQTMe9Sx'

def cleanhtml(raw_html):
    cleanr = re.compile('<.*?>')
    cleantext = re.sub(cleanr, '', raw_html)
    return cleantext


def getUrl(title,display=None,start=None):
    #The internal system will recognize foregin languages  as special charcaters,which leads to UnicoderError
    #unless the are correctly quoted. 
    title=urllib.parse.quote(title)
    
    if (display !=None and start ==None):
        myurl=DISPLAY %(title,display)
    elif (display !=None and start !=None):
        myurl=START %(title,display,start)
    else:
        myurl=BASEURL %(title)
    
    return myurl


def findItem(items,index,score_results):
    if len(items)==0:
        print("No Result")
        sys.exit(1)
    else:
        for item in items:
            link=item['link']
            result=re.split('code=',link)[1]
            score_results[index]={'title_KOR':cleanhtml(item['title']),'title_ENG':item['subtitle'],'link_code':result\
                                  ,'user_rating':item['userRating']}
            index+=1
    return score_results,index
    

def searchByTitle(titles,display=None,start=None):
    assert type(display)==int,'display must be integer'
    assert type(start)==int,'start must be integer'
    
   
    score_results={}
    index=0
    for title in titles:
        myurl=getUrl(title,display,start)
        header_params = {"X-Naver-Client-Id":client_id, "X-Naver-Client-Secret":client_secret}
        response=requests.get(myurl,headers=header_params)
        if response.status_code==200:
            data=json.loads(response.text)['items']
            result,index=findItem(data,index,score_results)
        else:
            logging.error(response.text)
            sys.exit(1)
    return result



genre_list={1:'drama', 2:'fantasy',3:'western',4:'horror',5:'romance',6:'adventure', 7:'thriller',8: 'noir'\
 ,9:'cult',10:'documentary',11:'commedy',12:'family',13:'mystery',14: 'war',15:'animation',16: 'criminal'\
 ,17:'musical',18:'SF',19:'action',20: 'martial arts',21:'erotic films',22:'suspense',23:"narrative"\
 ,24:'dark commedy',25:'experimental film',26: 'animated films',27:'musical',28:'paradies'}


def cycle(obj,score_results,index):
    for page in range(1,no_pages):
                info=obj.find_all('div',{'class':'score_result'})[0].find_all('li')
                for li in info:
                    score_results[count]={'score':int(li.em.text),'text':li.p.text.strip()\
                                      ,'critics_score':critic,'code':code,'details':details}
                    count+=1
    return score_results,index
    

def getComments(codes,no_pages=2):
    BASEURL='https://movie.naver.com/movie/bi/mi/basic.nhn?code=%s'
    count=0
    score_results=dict()
 
    for code in codes:
        url=BASEURL %code
        res=requests.get(url.format(1))
        obj=bs4.BeautifulSoup(res.text)
        info=obj.find_all('div',{'class':'score_result'})
        #if the serach does not contain information on comments,just discard immediately.
        if len(info)==0:
            continue
        #Preprocessing for this feature is required in the later stages
        details=obj.find('dl',class_='info_spec').select('dd > p > span > a')
        try:
            critics_score=obj.find_all('span',class_='st_off')[1]
            critic=re.search('[0-9.%]+',str(critics_score)).group()
        except:
            critic=np.nan
        for page in range(1,no_pages):
            info=obj.find_all('div',{'class':'score_result'})[0].find_all('li')
            for li in info:
                score_results[count]={'score':int(li.em.text),'text':li.p.text.strip()\
                                  ,'critics_score':critic,'code':code,'details':details}
                count+=1
    return score_results

data=searchByTitle(['광해','왕의 남자','Home Alone'],display=10,start=1)
data=pd.DataFrame(data).T


link=data.link_code.unique()
print(link)
getComments(link)
```
