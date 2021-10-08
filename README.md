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

