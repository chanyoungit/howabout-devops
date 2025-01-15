<div align="center">
  <img src="https://github.com/user-attachments/assets/b7d1d466-8b8c-4dca-ae70-75978bf01007" alt="KakaoTalk_Photo_2024-12-16-20-33-05" />
</div>

<div align="center">

### 팀명 : 삼삼오오

| 정우용(Woo.jeong) | 박찬영(Ayaan.park) | &nbsp;&nbsp;&nbsp;&nbsp;고경훈(K.ko)&nbsp;&nbsp;&nbsp;&nbsp; | &nbsp;김도현(Bruce.kim)&nbsp; | &nbsp;박설(Sunny.park)&nbsp; |
|:-------------------------------------------:|:--------------------------------------------:|:------------------------------------------:|:------------------------------------------:|:-------------------------------------------:|
| - 팀장 <br> - AI | - DevOps <br> | - DevOps <br> | - Front-end <br> | - Back-end <br> |

 </div>

 <br>

## 💁‍♂️ Detail Role <a name = "role"></a>
+ [정우용(Woo.jeong)](https://github.com/jwywoo)
  - As 팀장
    - 프로젝트 기획 및 일정 조정
  - As AI Engineer
    - Service Repository: 사용자가 사용할 수 있는 수준의 API 서버 및 RAG 저장소
      - [RAG API Repository](https://github.com/HowwAbout/RAG-API)
      - 구현 코드 및 설명이 포함된 REAMD.md 포함
    - Develop Repository: 사용자가 사용 이전 로컬 기능 MVP구현과 로직 테스트를위한 개발 단계에서의 저장소 모음
      - Retrieval Augmented Generation(RAG) 구현 -> [RAG 구현 과정](https://github.com/jwywoo/RAG)
      - 사용자 요청에 따른 데이트 계획, 일정 추천 및 생성
      - 데이트 생성 기준 및 데이트에 사용될 장소 크롤링 -> [HowAbout Data Crawler](https://github.com/jwywoo/RAG-Data/tree/main/ha-crawler)
        - 위치
        - 사용자 선호 활동
      - RAG Application Server 구현 -> [RAG 서버 구현](https://github.com/jwywoo/RAG/tree/main/rag-service/rag-api-server)
        - FastAPI 활용
        - 대용량 요청으로 인한 TPM 제한 예방을 위한 Exponential Backoff 로직 적용 -> [구현 레포](https://github.com/jwywoo/RAG/tree/main/rag-optimization)
<Br>

+ [박찬영(Ayaan.park)](https://github.com/chanyoungit)
  - Cloud
  - 아키텍처 설계 및 구현

<Br>

+ [고경훈(K.ko)](https://github.com/42kko)
  - Cloud
  - 아키텍처 설계 및 구현

<Br>

+ [김도현(Bruce.kim)](https://github.com/Dorae0)
  - Front-end
  - 모든 Front-end 구현

<Br>

+ [박설(Sunny.park)](https://github.com/lxeso)
  - Back-end
  - SpringSecurity와 jwt 이용한 사용자 인증 구현
  - 사용자들이 데이트 활동을 추가하고, 추가된 활동들로 데이트 계획을 작성할 수 있는 기능을 구현.
  - AI가 생성한 데이트 활동을 사용자가 직접 선택하여 계획에 추가할 수 있도록 하는 로직을 개발.
  - ManyToMany 연관관계를 풀어 중간 객체를 사용하여 데이트 활동을 다른 데이트 계획에서도 재사용 가능하도록 설계.
  - 데이트 계획 안에서 데이트 활동들의 순서를 관리하고, 오류 없이 처리되는 비즈니스 로직 구현.

<Br>


 <br>

# 🚩 프로젝트

<details>
   <summary> 본문 확인 (👈 Click)</summary>
<br />

### AI를 활용한 데이트 계획 작성 및 추천 서비스 HowAbout

- 데이트 계획을 세우기 어려운 사용자, 반복적인 데이트에 지친 커플, 또는 관계 초기 단계의 사람들을 위한 서비스
- 간단한 입력만으로 AI가 데이트 활동을 생성해주어 데이트 계획을 쉽게 작성 가능
- 사용자가 위치를 입력하면 해당 위치 기반으로 크롤링한 데이트 장소와 활동을 AI가 추천

</details>

<br>

# 🎁 결과물

<details>
   <summary> 본문 확인 (👈 Click)</summary>
<br />

### Main Page

<img width="1498" alt="KakaoTalk_Image_2024-12-16-21-02-07_001" src="https://github.com/user-attachments/assets/bfa0c56e-35e0-421a-8405-9ead4ad0fd8c" />

### AI Recommendation Page
<img width="1055" alt="KakaoTalk_Image_2024-12-16-21-02-07_002" src="https://github.com/user-attachments/assets/d2b26917-2208-49f8-a157-6c360d5ccfc3" />

</details>

<br>

# ☁️ 아키텍처

![image](https://github.com/user-attachments/assets/803d04cd-dc7d-4c5d-8124-16664034b323)

<br>

💡 본 프로젝트는 단순한 기능 구현뿐만이 아닌 애플리케이션의 사용자가 증가함에 따라 발생할 수 있는 트래픽 문제를 고려하여 진행했습니다.

### Jenkins

우선 Jenkins를 Master-Agent 구조로 분리했습니다. 초기에는 단일 서버에서 모든 빌드, 테스트, 배포 작업을 처리하던 방식이 성능상의 병목을 초래해 배포 시간이 길어졌습니다. 이를 해결하기 위해 Master 서버는 작업 스케줄링에 집중하고, Agent 서버에서 빌드와 테스트를 병렬로 처리하도록 구조 분리시켰습니다. Agent 서버는 CI Agent 서버와 CD Agent 서버를 분리하여 젠킨스 Executor 수를 여유롭게 가져가 다수의 파이프라인이 실행되어도 병목이 초래하지 않도록 구현했습니다. 또한, CI/CD Agent 서버는 스팟 인스턴스를 활용하여 파이프라인이 실행이 되었을 때 스팟 인스턴스로 서버를 생성하여 비용을 절감하고 스팟 인스턴스 기본 셋팅을 AMI를 자체 제작하여 배포 시간을 단축시켰습니다.

<br>

### Jenkins를 활용한 CI/CD 파이프라인

개발자가 소스 코드를 Push하여 Github에 PR이 발생하면 Jenkins 서버로 hook을 날려 파이프라인이 실행됩니다. Master 서버가 스팟 인스턴스로 AMI를 활용하여 CI/CD Agent서버를 생성합니다. CI Agent 서버는 도커파일을 이용하여 이미지를 생성하고 AWS ECR에 업로드합니다. 이후 CD Agent 서버가 업로드한 ECR 이미지를 활용하여 배포된 서버가 이미지를 Run합니다. 

<br>

### S3 & CloudFront & Route 53 배포

S3는 데이터 용량에 따라 비용이 청구되므로 적은 트래픽을 다루는 경우 매우 경제적이라고 생각이 들어 S3을 사용하여 서버 없이 비용을 효율적으로 프론트엔드 서버를 배포하였습니다.
CloudFront를 이용하여 전 세계에 분산된 엣지 로케이션에서 콘텐츠를 캐시하여 S3에서 데이터를 직접 가져오는 것보다 더 빠르고 효율적인 콘텐츠를 제공하도록 했습니다.
S3와 CloudFront는 자동으로 트래픽을 처리할 수 있어, 서버를 따로 관리하지 않고도 대규모 사용자가 동시에 접속할 수 있어 이 점도 고려했습니다.
Route 53을 사용하여 도메인을 S3와 CloudFront에 연결하여 사용자가 보다 접근하기 쉽도록 했습니다.

<br>

### 보안

프론트와 Nginx를 제외하고 Back-end, AI, DB, Monitoring 서버 등은 전부 Private Subnet으로 설정하여 외부에서 접근할 수 없도록 설정했습니다. NAT Gateway를 구성하여 나머지 Private Subnet 리소스가 인터넷으로 트래픽이 통할 수 있도록 연결했습니다.

<br>

### Nginx

Nginx의 리버스 프록시를 통해 Private Subnet으로 설정되어있어 외부에서 접근하지 못하는 서버에 접근을 하며, 또한 로드 밸런싱 및 무중단 배포를 활용하여 고가용성을 유지했습니다.

<br>

### Prometheus & Grafana

<br>

### 볼륨을 통한 DB 관리

<br>

### 개발 서버와 배포 서버 분리


