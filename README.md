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
# API 명세

### REST API
|   End point   	| HTTP Method 	| Description 	| Status 	|
|:-------------:	|:-----------:	|:-----------:	|:------:	|
|  /upload 	|     POST    	|   CSV데이터 업로드  	|  200  	|

---

### GraphQL API
#### 뮤테이션 (Mutations)

1. **addCategoryValue**
   ```graphql
   mutation AddCategoryValue($id: ID!, $labeler: ID!, $label: String!) {
     addCategoryValue(_id: $id, labeler: $labeler, label: $label)
   }
   ```

2. **addMasterSignUp**
   ```graphql
   mutation AddMasterSignUp($name: String!, $password: String!) {
     addMasterSignUp(name: $name, password: $password) {
       id
       name
     }
   }
   ```

3. **addTask**
   ```graphql
   mutation AddTask($name: String!, $kind: String!, $labelers: [AddLabelerInput], $status: Boolean, $totalVideos: Int, $expiration_date: Date, $doneVideos: Int) {
     addTask(name: $name, kind: $kind, labelers: $labelers, status: $status, totalVideos: $totalVideos, expiration_date: $expiration_date, doneVideos: $doneVideos) {
       id
       name
     }
   }
   ```

4. **addTaskToLabeler**
   ```graphql
   mutation AddTaskToLabeler($email: String!, $id: ID!, $name: String!) {
     addTaskToLabeler(email: $email, _id: $id, name: $name) {
       id
       name
     }
   }
   ```

5. **deleteLabelers**
   ```graphql
   mutation DeleteLabelers($id: ID!) {
     deleteLabelers(_id: $id) {
       id
     }
   }
   ```

6. **deleteTask**
   ```graphql
   mutation DeleteTask($name: String!) {
     deleteTask(name: $name) {
       id
     }
   }
   ```

7. **deleteTaskOfLabeler**
   ```graphql
   mutation DeleteTaskOfLabeler($email: String!, $id: ID!, $name: String!) {
     deleteTaskOfLabeler(email: $email, _id: $id, name: $name) {
       id
       name
     }
   }
   ```

8. **labelerLogIn**
   ```graphql
   mutation LabelerLogIn($email: String!, $googleId: String!, $name: String!, $idToken: String!) {
     labelerLogIn(email: $email, googleId: $googleId, name: $name, idToken: $idToken) {
       id
       name
     }
   }
   ```

9. **masterLogIn**
   ```graphql
   mutation MasterLogIn($name: String!, $password: String!) {
     masterLogIn(name: $name, password: $password) {
       id
       name
     }
   }
   ```

10. **updateTask**
    ```graphql
    mutation UpdateTask($name: String!, $newName: String, $kind: String, $labelers: [AddLabelerInput], $status: Boolean, $expiration_date: Date) {
      updateTask(name: $name, newName: $newName, kind: $kind, labelers: $labelers, status: $status, expiration_date: $expiration_date) {
        id
        name
      }
    }
    ```

#### 쿼리 (Queries)

1. **getAllLabelers**
   ```graphql
   query GetAllLabelers {
     getAllLabelers {
       id
       name
       email
     }
   }
   ```

2. **getAllTasks**
   ```graphql
   query GetAllTasks {
     getAllTasks {
       id
       name
       status
     }
   }
   ```

3. **getLabelersTasks**
   ```graphql
   query GetLabelersTasks($id: ID!) {
     getLabelersTasks(_id: $id) {
       id
       name
       status
     }
   }
   ```

4. **getRandomVideo**
   ```graphql
   query GetRandomVideo($labeler: String!, $taskName: String!) {
     getRandomVideo(labeler: $labeler, taskName: $taskName) {
       id
       url
     }
   }
   ```

5. **getTaskDetail**
   ```graphql
   query GetTaskDetail($id: ID!, $name: String) {
     getTask
    Detail(_id: $id, name: $name) {
       id
       name
       status
     }
   }
   ```

6. **searchLabeler**
   ```graphql
   query SearchLabeler($id: ID!) {
     searchLabeler(_id: $id) {
       id
       name
       email
     }
   }
   ```

7. **searchLabelerByGId**
   ```graphql
   query SearchLabelerByGId($googleId: String!) {
     searchLabelerByGId(googleId: $googleId) {
       id
       name
       email
     }
   }
   ```
   
8. **masterLogIn**
   ```graphql
   query MasterLogIn($name: String!, $password: String!) {
     masterLogIn(name: $name, password: $password) {
       id
       name
     }
   }
   ```
