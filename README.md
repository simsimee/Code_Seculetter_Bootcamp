# Malicious-PDF-classification

## 악성 PDF 파일 분류

### 프로젝트 개요
- 코드스테이츠 AI부트캠프 과정 중 '시큐레터' 기업과의 협업으로 진행하게 된 프로젝트

![image](https://user-images.githubusercontent.com/75903850/136335506-42500eb2-fd72-40e2-bdd6-4cd8612a6812.png)
- 문서형 악성코드는 주로 이메일이나 웹사이트의 첨부된 파일을 통해 사용자 모르게 다운되는 악성코드이고 APT(지능형 지속 공격 기법)의 공격 수단으로 문서형 악성코드가 자주 사용된다.

![image](https://user-images.githubusercontent.com/75903850/136338107-f9899bc4-44e8-4c77-bb22-da14e808230a.png)
- APT는 불특정 다수를 대상으로 하는 기존공격과 다르게 목표를 정하고 침투가 성공할 때까지 공격하는 기법이다. APT는 위의 표처럼 굉장히 이슈가 될만하고 클릭하고 싶게 만드는 사회공학 기법을 활용하기 때문에 이에 적합한 문서형 악성코드가 자주 활용된다.

![image](https://user-images.githubusercontent.com/75903850/136344022-798df59a-fe83-4886-a69f-596f31bebcce.png)
- 이는 문서형 악성코드로 발생한 국내 침해사고 중 대표적인 사례이다. 해커가 퇴직자의 정보를 이용해 정보 탈취용 문서형 악성코드를 첨부해 피싱 메일을 보내고 약 만 명의 개인정보가 유출된 사건이다. 이처럼 대부분의 문서형 악성코드는 PDF나 한글파일 형태가 대부분이라고 알려져있고 이 중 PDF를 악성파일, 정상파일로 분류하는 프로젝트를 기획

### 참고 논문
1. [Detection of Malicious PDF based on Document Structure Features and Stream Objects](https://www.koreascience.or.kr/article/JAKO201809355933293.pdf)/ 2018.11.30 / Kang, Ah Reum 외 5명
2. [Data Mining Based Strategy for Detecting Malicious PDF Files](https://ieeexplore.ieee.org/document/8455965)/ 2018.09.06 / Samir G. Sayed, Mohmed Shawkey
3. [Hidost: a static machine-learning-based detector of malicious files](https://link.springer.com/content/pdf/10.1186/s13635-016-0045-0.pdf)/ 2016.09.26 / Nedim Šrndić & Pavel Laskov 
4. [Detection of malicious PDF files and directions for enhancements: A state-of-the art survey](https://www.sciencedirect.com/science/article/pii/S0167404814001606?casa_token=ewyvSRQBFmkAAAAA:DpxW4KmaPbM0oe8n6z2oObI7eIzUsVuwhGz_gy8gSqLstniQhuwShjqFT-je9Ol7T7AY_MZ4VXA)/ 2014.10.23 / Nir Nissim, Aviad Cohen, Chanan Glezer, Yuval Elovicia
5. [A structural and content-based approach for a precise and robust detection of malicious PDF files](https://ieeexplore.ieee.org/abstract/document/7509925?casa_token=pCxlt1XsOoEAAAAA:3_QC0TeTuFg49lV46evto3db1HCUMqTcYczFHYCX-3bQmo_6XPdI7_YVUJPEu1CZxeynzQTt974)/ 2016.06.14 / Davide Maiorca, Davide Ariu, Igino Corona, Giorgio Giacinto

### 가설
악성 PDF 파일은 정상 PDF 파일과 구조적으로 다른 점이 있을 것이다. PDF파일의 특성을 추출하여 악성 PDF를 분류해낼 수 있다.

### 데이터셋
![image](https://user-images.githubusercontent.com/75903850/136900239-006ff90f-0467-40d6-b8d9-0eff7c900996.png)    

데이터는 시큐레터 기업에서 제공해주셨고 정상 PDF 문서 7674개, 악성 PDF 3011개의 PDF 문서로 이루어진 데이터.
분류기준모델의 정확도 : 0.72

### PDF feature extraction
- 사용한 pdf parser : pikepdf. 팀프로젝트로 개인간 다른 parser를 이용하여 feature extraction 진행
- pikepdf는 PDF를 생성, 조작, 구문 분석, 복구 등을 위한 라이브러리
- pikepdf_parser.ipynb 파일에서 진행하였으며 총 552개의 feature 를 추출

### 비정형 데이터 -> 정형 데이터
- json형태로 feature를 추출하였고 json을 csv파일로 변환
- csv파일 형태를 dataframe으로 변환
- pikepdf_feature.ipynb, model.ipynb 파일에서 진행

### feature selection (여기서부터 model.ipynb 파일에서 진행)
- 결측치가 60%이상인 feature 삭제
- 이름이 비슷한 중복 feature 삭제
- 최종적으로 13개의 feature selection

#### 특성 상관계수
![image](https://user-images.githubusercontent.com/75903850/136902218-27339c66-1673-428d-a529-51877db6f4f8.png)

### 데이터 전처리
- Size, Contents_Length 등 숫자형 데이터는 결측치 0
- Author, Producer, PDFversion 등 범주형 데이터는 결측치를 'nan' 이라는 문자로 변환 (해당 정보를 포함하고있지 않은 것도 악성 PDF의 특성이 될 수 있겠다고 생각)
- 범주형 데이터는 TargetEncoder를 사용하여 encoding 진행
- MinMaxScaler를 이용하여 데이터 스케일링

### 분류모델
<img width="646" alt="스크린샷 2021-10-12 오후 3 30 22" src="https://user-images.githubusercontent.com/75903850/136903665-88311453-ce3b-4f22-bc9b-ee5b48ad4cef.png">
- RandomForest, XGBoost, SVM 세 가지 모델을 validation set 으로 검증한 결과 비교    
- f1-score와 accuracy가 조금 더 앞서는 RandomForest 모델로 결정
- 최종모델로 Randomized SearchCV 로 하이퍼파라미터 튜닝
<img width="461" alt="스크린샷 2021-10-12 오후 3 34 00" src="https://user-images.githubusercontent.com/75903850/136904115-34eae127-a4bd-4c15-85cd-c24fe82fa9a0.png">
- test set 분류 결과 precision 0.92, recall 0.97, f1-score 0.94, accuracy 0.92

### feature importance
![image](https://user-images.githubusercontent.com/75903850/136904656-b000142f-471b-4f24-b1f3-a984ba06c663.png)
![image](https://user-images.githubusercontent.com/75903850/136904673-2996eff2-1290-48ef-8e20-3bc24845f8c6.png)
- Producer, Creator 는 Word, PPT, Adobe pdf 같은 어떤 확장자를 이용했는지와 컨텐츠의 길이, pdf의 크기 등이 가장 중요했음을 알 수 있었다.

### 개선 방향
- Pikepdf 모듈만 사용하는게 아니라 다른 pdf parser도 같이 이용해서 더 다양한 feature를 추출하고 그중에서 선택했으면 더 좋은 성능을 낼 수 있지 않았을까 싶고 모델의 Scoring을 recall에 좀 더 초점을 두어서, 악성 PDF를 정상으로 잘못 분류하지 않는 것이 악성 PDF에 대한 위험도를 조금 더 줄일 수 있을 것이라 생각함.
