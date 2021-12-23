# Today I Learned

> Fast API 공식 문서를 보고 정리합니다.:pencil2:

- [공식 문서](https://fastapi.tiangolo.com/ko/)
- [공식 문서 - 튜토리얼](https://fastapi.tiangolo.com/ko/tutorial/)

## 설치

```bash
$ pip install fastapi
$ pip install uvicorn[standard]
```

## 실행

```bash
$ uvicorn main:app --reload
```

- `main` : 파일 main.py

- `app` : main.py 내부에서 생성한 오브젝트

  ```python
  app = FastAPI()
  ```

  app이 아니라 다른 이름으로 만들 수 있고, 서버 실행할 때 해당 이름을 사용하면 됨

- `--reload` : 코드 변경 후 서버 재시작

### 예제

```python
from fastapi import FastAPI # 1. FastAPI 임포트
from typing import Optional

app = FastAPI() # 2. FastAPI 인스턴스 생성

# 3. 경로 동작 데코레이터 작성
@app.get("/") # 경로 /로 GET 요청 받기
# 4. 경로 동작 함수 작성
def read_root():
    return {"Hello": "World"} # 5. 콘텐츠 반환

@app.get("/items/{item_id}")
def read_item(item_id: int, q: Optional[str] = None): # int 경로 매개변수 item_id, 선택적인 str형 경로 매개변수 q를 가지고 있음
    return {"item_id": item_id, "q": q}
```

- `@app.get("/")` : 경로 동작 **데코레이터**
  - FastAPI에게 바로 아래에 있는 함수가 다음으로 이동하는 요청을 처리한다는 것을 알려줌
  - post, put, delete 등 다른 동작도 쓸 수 있음

- 아래의 링크로 들어가면 각 경로에 맞는 JSON 응답을 볼 수 있음
  1. http://127.0.0.1:8000/
  2. http://127.0.0.1:8000/items/5?q=somequery

## API 문서

- Swagger UI : http://127.0.0.1:8000/docs
- ReDoc : http://127.0.0.1:8000/redoc




