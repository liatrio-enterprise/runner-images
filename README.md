# GitHub Actions Self-Hosted Runner Images

This is a monorepo for customized build agent images.

### The following images are currently available:

- [dotnet-sdk-3.1](.github/workflows/dotnet-sdk-3.1.yaml)
- [nodejs-12](.github/workflows/nodejs-12.yaml)
- [terraform-1.0](.github/workflows/terraform-1.0.yaml)

#### Check out the org [packages](https://github.com/orgs/liatrio-enterprise/packages?ecosystem=container) for up-to-date tags.

Each image has its own workflow, which will be triggered when a file in the respective image's directory is updated.
These workflows utilize a [reusable workflow](https://github.com/liatrio-enterprise/github-workflows/blob/main/.github/workflows/docker-build-conventional.yml) 
that will build and push the image, and use conventional commits to create git and image tags.

## Adding a new image
1. Add a new folder at the root of the repo to hold the Dockerfile and any other files needed for the image
    * If the image will support long-lived major versions (for example multiple major versions of node), consider nesting directories for the major versions:
      ```shell
      /
      nodejs/
        12/
          Dockerfile
        14/
          Dockerfile
      ```
2. Add a workflow for the new image under `.github/workflows`
    * If supporting multiple versions, there should be a workflow per long-lived/major version.

   Example for nodejs 14:

    ```yaml
    on:
      push:
        branches:
          - main
        paths:
          - "nodejs/14/**"
      pull_request:
        branches:
          - main
        paths:
          - "nodejs/14/**"
      workflow_dispatch: 
    
    name: Node.js 14 build 
    
    jobs:
      Release:
        uses: liatrio-enterprise/github-workflows/.github/workflows/docker-build-conventional.yml@main
        with:
          directory: "nodejs/14"
          tagPrefix: "nodejs-14"
          imageName: "ghcr.io/liatrio-enterprise/runner-images/nodejs-14"
   ```