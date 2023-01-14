## pickle
```python
import pickle
 
name = 'james'
age = 17
address = '서울시 서초구 반포동'
scores = {'korean': 90, 'english': 95, 'mathematics': 85, 'science': 82}
 
with open('james.p', 'wb') as file:    # james.p 파일을 바이너리 쓰기 모드(wb)로 열기
 
    pickle.dump(name, file)
    pickle.dump(age, file)   
    pickle.dump(address, file)
    pickle.dump(scores, file)    


with open('james.p', 'rb') as file:
    try:        
        while f:=pickle.load(file):
            print(f)
    except:
        pass
```