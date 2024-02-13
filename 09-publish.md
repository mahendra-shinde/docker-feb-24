# Publish Images to Registry

- Signup on docker-registry (Docker Hub)

    - Use Personal Email to Signup
    - Open Inbox and use the `Activation Link` to activate your new docker-hub.

- Login with Docker CLI

    ```
    docker login -u ACCOUNT-NAME
    Password >> ENTER-PASSWORD
    ```

- Rename your image to include ACCOUNT-NAME as prefix

    ```bash
    # docker tag aspapp ACCOUNT-NAME/aspap
    docker tag aspapp mahendrshinde/aspapp
    docker push mahendrshinde/aspnet
    ```
