# blind-review-parser
블라인드의 기업 리뷰를 파싱한 뒤 ES 에 색인하는 스크립트

<br>

## 블라인드 기업 리뷰?
- Page: https://www.teamblind.com/kr/company
- Review sample (구글코리아)

    ![구글코리아 공개 리뷰정보](https://user-images.githubusercontent.com/20942871/107968678-01544200-6ff2-11eb-88b9-2c2c65afb387.png)


>### ⚠ Disclaimer
> 리뷰 전체 상세내용을 확인하기 위해선 로그인 & 본인 기업 리뷰가 필요하기 때문에, **리뷰 제목과 평점, 직군 등의 오픈된 정보만 수집**하였습니다.


<br>


## Kibana chart examples

- 아래 차트는 2020-07-01 ~ 2021-02-16 까지 작성된 리뷰 데이터로 생성되었습니다.

<br>

### NAVER 기업 분석 차트
![image](https://user-images.githubusercontent.com/20942871/108037207-9865dc00-707c-11eb-86dc-f8ae1112be8d.png)


<br>

### 3대 통신사 비교 차트
![image](https://user-images.githubusercontent.com/20942871/108037523-132ef700-707d-11eb-847a-a5368af82085.png)


<br>

## How to use?

#### 1. Elasticsearch & Kibana 실행
- 참고: https://www.elastic.co/kr/start

#### 2. Blind 기업 리뷰 수집 & ES 색인

1. [`blind_review_parser.py`](https://github.com/occidere/blind-review-parser/blob/main/blind_review_parser.py) 파일 내 `companies` 리스트에 블라인드에 등록된 기준의 회사명을 입력
2. `es_endpoint` 에 리뷰를 저장할 Elasticsearch 주소 입력 후 실행

```python
if __name__ == '__main__':
    companies = [
        'NAVER', '카카오', '라인플러스', 'COUPANG', '우아한형제들',  # 네카라쿠배
        'NEXON', '넷마블', 'NCSOFT'  # 3N
    ]
    for c in companies:
        blind_parser = BlindParser(company=c, es_endpoint='http://localhost:9200')
        blind_parser.run()
```

#### 3. [`blind_review_saved_object.ndjson`](https://github.com/occidere/blind-review-parser/blob/main/blind_review_saved_object.ndjson) 파일 import
- Kibana 에서 Stack Management > Saved objects 메뉴
<img src="https://user-images.githubusercontent.com/20942871/108064772-7bdb9b00-70a0-11eb-839b-50fe0b018b49.png" width="60%" />

#### 4. Kibana 의 Analytics 메뉴에서 Visualize / Dashboard 확인
