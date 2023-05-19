<!-- start title -->

# GitHub Action:Build and Push Image to ECR

<!-- end title -->
<!-- start description -->

Builds and pushs an image to an AWS ECR repository

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: catalystsquad/action-build-push-image-ecr@undefined
  with:
    # Name of ECR repository to push images to. Defaults to the Git repository's name.
    # Default: ${{ github.repository }}
    ecr-repository: ""

    # AWS secret key ID. Required.
    aws-access-key-id: ""

    # Skip AWS session tagging for the role assumption step
    # Default: false
    role-skip-session-tagging: ""

    # AWS secret access key. Required.
    aws-secret-access-key: ""

    # AWS region. Required.
    aws-region: ""

    # AWS IAM role to assume.
    role-to-assume: ""

    # AWS IAM role external id
    role-external-id: ""

    # AWS IAM role assumption duration seconds
    # Default: 900
    role-duration-seconds: ""

    # Creates the ECR repository if it does not exist
    # Default: true
    create-missing-repositories: ""

    # AWS IAM role assumption session name
    # Default: action-build-push-image-ecr
    role-session-name: ""

    # List of AWS accounts to add access for
    # Default:
    extra-account-access: ""

    # git tags to push, comma separated string such as `latest,v1.0.0`
    # Default: latest,${{ github.event.release.tag_name }}
    tag-versions: ""

    # docker build secrets. key=value pairs separated by newlines. See [docker build
    # push action secrets configuration](https://github.com/docker/build-push-action/blob/master/docs/advanced/secrets.md) for details
    # Default:
    build-secrets: ""

    # docker context. Passed to [docker build push action context
    # input](https://github.com/docker/build-push-action#inputs). It should be
    # relative to the root of the commit that triggered the action
    # Default: ./
    docker-context: ""

    # path to docker file relative to docker-context. Passed to [docker build push
    # action file input](https://github.com/docker/build-push-action#inputs)
    # Default: Dockerfile
    docker-file: ""
```

<!-- end usage -->
<!-- start inputs -->

| **Input**                         | **Description**                                                                                                                                                                                                 |                  **Default**                  | **Required** |
| :-------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------: | :----------: |
| **`ecr-repository`**              | Name of ECR repository to push images to. Defaults to the Git repository's name.                                                                                                                                |          `${{ github.repository }}`           |  **false**   |
| **`aws-access-key-id`**           | AWS secret key ID. Required.                                                                                                                                                                                    |                                               |   **true**   |
| **`role-skip-session-tagging`**   | Skip AWS session tagging for the role assumption step                                                                                                                                                           |                                               |  **false**   |
| **`aws-secret-access-key`**       | AWS secret access key. Required.                                                                                                                                                                                |                                               |   **true**   |
| **`aws-region`**                  | AWS region. Required.                                                                                                                                                                                           |                                               |   **true**   |
| **`role-to-assume`**              | AWS IAM role to assume.                                                                                                                                                                                         |                                               |  **false**   |
| **`role-external-id`**            | AWS IAM role external id                                                                                                                                                                                        |                                               |  **false**   |
| **`role-duration-seconds`**       | AWS IAM role assumption duration seconds                                                                                                                                                                        |                     `900`                     |  **false**   |
| **`create-missing-repositories`** | Creates the ECR repository if it does not exist                                                                                                                                                                 |                    `true`                     |  **false**   |
| **`role-session-name`**           | AWS IAM role assumption session name                                                                                                                                                                            |         `action-build-push-image-ecr`         |  **false**   |
| **`extra-account-access`**        | List of AWS accounts to add access for                                                                                                                                                                          |                                               |  **false**   |
| **`tag-versions`**                | git tags to push, comma separated string such as `latest,v1.0.0`                                                                                                                                                | `latest,${{ github.event.release.tag_name }}` |  **false**   |
| **`build-secrets`**               | docker build secrets. key=value pairs separated by newlines. See [docker build push action secrets configuration](https://github.com/docker/build-push-action/blob/master/docs/advanced/secrets.md) for details |                                               |  **false**   |
| **`docker-context`**              | docker context. Passed to [docker build push action context input](https://github.com/docker/build-push-action#inputs). It should be relative to the root of the commit that triggered the action               |                     `./`                      |  **false**   |
| **`docker-file`**                 | path to docker file relative to docker-context. Passed to [docker build push action file input](https://github.com/docker/build-push-action#inputs)                                                             |                 `Dockerfile`                  |  **false**   |

<!-- end inputs -->
<!-- start outputs -->

| **Output**      | **Description** | **Default** | **Required** |
| :-------------- | :-------------- | ----------- | ------------ |
| `random-number` | Random number   |             |              |

<!-- end outputs -->
<!-- start examples -->

### Example usage

```yaml
name: Build and push image to ECR
on:
  release:
    types: [created]
jobs:
  build-push-image:
    runs-on: ubuntu-latest
    steps:
      - uses: catalystsquad/action-build-push-image-ecr@v1
        with:
          aws-access-key-id: ${{ secrets.AUTOMATION_AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AUTOMATION_AWS_SECRET_ACCESS_KEY }}
          role-to-assume: arn:aws:iam::000000000000:role/YourRoleHere
          aws-region: us-west-2
          extra-account-access: 000000000000,111111111111,222222222222
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->
