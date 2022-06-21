## About


An internal repo to demo Lacework CI workflow implementations leveraging:
- [The Lacework Inline Scanner](https://docs.lacework.com/integrate-the-lacework-inline-scanner-with-ci-pipelines) in a GitHub Action workflow
- Lacework Policy Evaluator in CI Piplines (alpha/beta)
  - See [Tech Talk on Our DevSecOps story (11/05/21)](https://lacework.atlassian.net/wiki/spaces/ENG/pages/2312110131/Tech+Talks#%5Bdate%5D---Shifting-Security-Left---Our-DevSecOps-Story-by-%40Chitra-Kumar-%40Divyang-Soni)

# Voting App

This sample creates a multi-container application. The application interface has been built using Python / Flask. The data component is using Redis.

To walk through a quick deployment of this application, see the Microsoft Tutorial [doc](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app).

## Run locally

### Run kubectl
1. View services
- kubectl svc
2. Apply yaml files
- kubectl apply -f .
3. Expose port for local host: 
- kubectl port-forward voting-service-front-74c6d68576-5vvwm 8080:80  

## Prerequisites

1. The Policy Evaluateor in this demo requires 2 secrets to be generated:

| Secret Name | Value Required |
|-------------      |--------------- |
|LW_ACCESS_TOKEN                     | Access token from a Container Registry integration for the `Inline Scanner` |
|LW_ACCOUNT_NAME                     | LW Instance rule where Access Token and Policies are defined from |

2. Configure Container Policies within the Lacework Platform for *Action on Failure*: `Block` 

## How to Demo
1. Open project in Codespaces or VS Code
2. Use `docker-compose build` and `docker-compose up` commands to show off the application
3. Create a new branch, 
    - modify `voting-service/voting-service/config_file.cfg` to update homepage values
    - modify IaC to introduce violations in folders `terraform` , `manifests` , or `CloudFormation`
1. Create a PR from the new branch to the `main` branch
3. View the GitHub Action workflow run for the LW Inline scanner and view the check failed due to a policy violation


# Troubleshooting / Limitations

## Manifest File
Currently the `manifests/deployment.yml` file needs to have the `voting-service-front` **image** value updated to match your repository.

# References
