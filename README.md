# 버즈앤비 기업협업 프로젝트

## 프로젝트 소개

이 프로젝트는 사내 머신러닝 모델의 지도학습을 위한 데이터 라벨링의 효율성과 정확성을 개선하기 위해 데이터의 정확성을 판별하는 라벨링 앱과 라벨러 할당과 관리를 위한 백오피스 웹을 개발하는 프로젝트입니다.

## 개발 환경

- **개발 기간**: 2022/09/19 ~ 2022/10/13
- **개발 인원**: Front-end 3명, Back-end 2명


## 기술 스택
### Front-end
| Language | Framework | Authentication |
|----------|-----------|----------------|
| ![JavaScript](https://img.shields.io/badge/-JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=white) | ![React.js](https://img.shields.io/badge/-React.js-61DAFB?style=flat&logo=react&logoColor=white) ![ReactNative](https://img.shields.io/badge/-ReactNative-61DAFB?style=flat&logo=react&logoColor=white) ![Next.js](https://img.shields.io/badge/-Next.js-000000?style=flat&logo=next.js&logoColor=white) ![GraphQL](https://img.shields.io/badge/-GraphQL-E10098?style=flat&logo=graphql&logoColor=white) ![Styled-Components](https://img.shields.io/badge/-StyledComponents-DB7093?style=flat&logo=styled-components&logoColor=white) | ![Google Authentication](https://img.shields.io/badge/-GoogleAuthentication-4285F4?style=flat&logo=google&logoColor=white) |
### Back-end
| Language | Framework | Database | Containerization | Cloud Service | Authentication |
|----------|-----------|----------|------------------|---------------|----------------|
| ![JavaScript](https://img.shields.io/badge/-JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=white) | ![GraphQL Apollo Server](https://img.shields.io/badge/-ApolloGraphQL-311C87?style=flat&logo=apollographql&logoColor=white) ![Express.js](https://img.shields.io/badge/-Express.js-000000?style=flat&logo=express&logoColor=white) | ![MongoDB](https://img.shields.io/badge/-MongoDB-47A248?style=flat&logo=mongodb&logoColor=white) | ![Docker](https://img.shields.io/badge/-Docker-2496ED?style=flat&logo=docker&logoColor=white) | ![AWS EC2](https://img.shields.io/badge/-AWSEC2-FF9900?style=flat&logo=amazonec2&logoColor=white) | ![Google Authentication](https://img.shields.io/badge/-GoogleAuthentication-4285F4?style=flat&logo=google&logoColor=white) |

## 프로젝트 관리 도구

| 도구 | 사용 목적 | 링크 |
|------|-----------|------|
| ![Trello](https://img.shields.io/badge/-Trello-0079BF?style=flat&logo=trello&logoColor=white) | 작업 진행 상황 관리 | https://trello.com/b/NlSZ1c5v/bzznbydwecode |
| ![Notion](https://img.shields.io/badge/-Notion-000000?style=flat&logo=notion&logoColor=white) | 문서화 및 정보 공유 |

---

## 백엔드 구현 기능

### 사용자 인증
- 마스터 계정과 일반 사용자 구글 소셜 회원가입 및 로그인
- JWT를 사용한 인증 시스템

### 라벨러 관리
- 전체 라벨러 조회
- 라벨러 상세조회
- 라벨러 검색
- 라벨러에게 할당된 테스크 조회

### 테스크 관리
- 전체 테스크 조회
- 테스크별 라벨러 조회
- 새로운 테스크에 라벨러 추가
- 테스크에 데이터 csv파일 업로드
- 각 테스크에 할당된 라벨러에게 알맞는 라벨링데이터 할당
- 테스크 수정
- 테스크 삭제
---

## 내가 개발한 기능
### 테스크 관리

- **어려웠던 부분**:
  - **비디오 할당 로직**: 프로젝트의 가장 복잡한 부분 중 하나는 비디오 할당 로직이었습니다. 관리자가 라벨러들을 새로운 테스크에 할당하면, 라벨러들은 모든 비디오 데이터가 라벨링될 때까지 계속해서 비디오 데이터를 할당받아 작업합니다. 각 비디오는 테스크에 할당된 라벨러 3명에 의해 라벨링이 완료되어야 했습니다. 그리고 각 테스크는 업로드 된 비디오 전부가 라벨링이 완료가 되어야 완료가 되는 구조였습니다. 이 로직의 구현 과정에서, 데이터 할당의 효율성과 정확성을 보장하기 위한 방안을 모색하는 데 어려움을 겪었습니다.
      - **문제점**: 초기 구현에서는 똑같은 라벨러가 하나의 비디오에 대해서 라벨링을 하거나, 하나의 비디오 데이터에 대해 3명 이상의 라벨러가 작업을 하고 완료해버리는 등 데이터 동시성 문제가 발생했습니다. 이로 인해 비디오 할당과 라벨링 작업의 정확성과 효율성이 저하되었습니다.
  
      - **해결 방안**: 이 문제를 해결하기 위해 먼저 각 비디오 별로 현재 작업 중인 라벨러의 ID를 저장하고 관리하도록 개선했습니다. 이를 통해 라벨러의 중복된 라벨링을 방지하고, 각 비디오에 대해 라벨링 중인 라벨러의 수를 카운트할 수 있게 되었습니다. 그러나 이러한 방식은 사용자의 요청마다 데이터베이스에 불필요한 데이터 조회 쿼리를 추가하여 처리하였으며, 이로 인해 데이터베이스의 빈번한 조회로 성능 저하를 일으키고 비효율적이었습니다.

      - **도전 과제**: 효율적인 해결 방안을 찾는 것이 도전적이었습니다. 데이터베이스 성능을 향상시키고 동시성 문제를 해결하는 최적의 방법을 찾기 위해 다양한 시도를 하였으나, 완벽한 해결책을 찾지 못한 채 문제에 대한 절충안을 도입했습니다.

- **아쉬운점**:
  - **CSV데이터 업로드 및 처리**: 테스크에 대한 대량의 데이터(csv 파일)를 데이터베이스에 업로드하고 처리하는 과정에서 서버에 파일을 저장하여 데이터를 읽은 후 파일을 삭제하는 불필요한 과정을 통했었는데, 스트림을 사용하면 대용량 파일을 효과적으로 처리할 수 있고, 서버의 메모리 사용을 최적화할 수 있을 거 같다.
  - **테스크 상태 관리**: 소켓을 사용해 실시간으로 라벨러 앱과 백오피스 웹에서 테스크의 상태를 업데이트하고 관리하는 기능을 구현하려고 했으나, 시간 부족으로 소켓통신을 사용하지 못했던 점.
 
---

# API

### REST API
|   End point   	| HTTP Method 	| Description 	| Status 	|
|:-------------:	|:-----------:	|:-----------:	|:------:	|
|  /upload 	|     POST    	|   CSV데이터 업로드  	|  200  	|

---

### GraphQL API
##### 쿼리 (Queries)
|   Query            | Description              | Status  |
|:------------------:|:------------------------:|:------: |
| getAllLabelers     | 모든 라벨러 조회         |  200   |
| getAllTasks        | 모든 테스크 조회         |  200   |
| getLabelersTasks   | 라벨러의 모든 테스크 조회 |  200   |
| getRandomVideo     | 무작위 비디오 조회       |  200   |
| getTaskDetail      | 테스크 상세 정보 조회    |  200   |
| searchLabeler      | 라벨러 검색              |  200   |
| searchLabelerByGId | Google ID로 라벨러 검색  |  200   |

##### 뮤테이션 (Mutations)
|   Mutation          | Description                 | Status  |
|:------------------:|:---------------------------:|:------: |
| addCategoryValue    | 카테고리 값 추가            |  200   |
| addMasterSignUp     | 마스터 계정 회원가입        |  201   |
| addTask             | 테스크 추가                 |  201   |
| addTaskToLabeler    | 라벨러에게 테스크 할당      |  200   |
| deleteLabelers      | 라벨러 삭제                 |  200   |
| deleteTask          | 테스크 삭제                 |  200   |
| deleteTaskOfLabeler | 라벨러의 테스크 삭제        |  200   |
| labelerLogIn        | 라벨러 로그인               |  200   |
| masterLogIn         | 마스터 로그인               |  200   |
| updateTask          | 테스크 업데이트             |  200   |

자세한 GraphQL 쿼리는 Backend 폴더의 [README.md](https://github.com/jungsae/bzznbyd/blob/main/Backend/README.md) 에 있습니다.
