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
