# CI CD Pipeline for DEV

On Push to
- dev branch
- feature/* branch

On Pull Request to
- dev branch
- feature/* branch

The pipeline will run unit test and integration test
1. Checkout the repository
2. Setup environment and run unit test
3. Run integration test
4. Build docker image and push to container registry
    - tag is suffixed with "-SNAPSHOT" if the branch is not main
5. Update tag version in YAML file of `Tsuweiquan/my-argocd-poc-gitops` repository in `main` branch
6. Argocd watching the gitops repository and will update the application in DEV environment automatically

# CI Pipeline for UAT

On Pull Request to
- main branch

The pipeline will run unit test and integration test
1. Checkout the repository
2. Setup environment and run unit test
3. Run integration test


# CD Pipeline for UAT
On Push to
- main branch

The pipeline will run unit test and integration test
1. Checkout the repository
2. Setup environment
4. Build docker image and push to container registry
    - tag is the version number of the application if the branch is main
5. Create a github tag of the application version
6. Create a github release from the tag
7. Update tag version in YAML file of `Tsuweiquan/my-argocd-poc-gitops` repository in `main` branch
8. Argocd watching the gitops repository and will update the application in UAT environment automatically

# CI CD Pipeline for PROD

On workflow dispatch manually on selected Tag
-> User must access to Github Repo and have permissions to run workflow dispatch
Actions -> PROD CI & CD -> Run workflow -> Select Tag

The pipeline will run unit test and integration test
1. Checkout the repository
2. Setup environment and run unit test
3. Run integration test
4. Update tag version in YAML file of `Tsuweiquan/my-argocd-poc-gitops` repository in `main` branch
5. Argocd watching the gitops repository is ready to sync the application to PROD environment but will not do so automatically. It will show Out Of Sync in argocd.
6. `<Pending manual sync from deployment team in argocd>`
7. Sync the prod application in argocd when ready to deploy the version to PROD environment