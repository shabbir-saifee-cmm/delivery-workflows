
### How to publish terraform rc automation

  ```
  name: Terraform RC Create Automation

  on:
    push:
      tags:
        - '0.0.0-terraform-*-*-rc*'  # Matches enforced RC tag pattern

  jobs:
    call-release-workflow:
      uses: shabbir-saifee-cmm/delivery-workflows/.github/workflows/terraform-release-candidate.yaml@main
      with:
        tagName: ${{ github.ref_name }}  # The tag name (e.g., "0.0.0-terraform-myapp-john-rc1")
        artifactConfig: |
          terraform:
            hcp-terraform:
              moduleName: hcp-terraform
              modulePath: ./terraform/hcp-terraform
              moduleProvider: tfe
      secrets:
        MCK_CMM_HCP_TERRAFORM_TOKEN: ${{ secrets.MCK_CMM_HCP_TERRAFORM_TOKEN }}
  ```

### How to publish terraform rc automation

```
name: RC Tag Terraform Module Publisher

on:
  push:
    tags:
      - '0.0.0-terraform-*-*-rc*'  # Matches RC tags created by workflow 1

jobs:
  call-release-workflow:
    uses: shabbir-saifee-cmm/delivery-workflows/.github/workflows/terraform-release-candidate.yaml@main
    with:
      releaseName: ${{ github.ref_name }}
      artifactConfig: |
        terraform:
          hcp-terraform:
            moduleName: hcp-terraform
            modulePath: ./terraform/hcp-terraform
            moduleProvider: tfe
    secrets:
      MCK_CMM_HCP_TERRAFORM_TOKEN: ${{ secrets.MCK_CMM_HCP_TERRAFORM_TOKEN }}
```
