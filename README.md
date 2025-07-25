@YeshwanthKumarN ➜ /workspaces/terraform-adv (main) $ unset GITHUB_TOKEN
@YeshwanthKumarN ➜ /workspaces/terraform-adv (main) $ echo $GITHUB_TOKEN

@YeshwanthKumarN ➜ /workspaces/terraform-adv (main) $ gh auth login -s delete_repo
? Where do you use GitHub? GitHub.com
? What is your preferred protocol for Git operations on this host? HTTPS
? Authenticate Git with your GitHub credentials? Yes
? How would you like to authenticate GitHub CLI? Login with a web browser

! First copy your one-time code: 
Press Enter to open https://github.com/login/device in your browser...
✓ Authentication complete.
- gh config set -h github.com git_protocol https
✓ Configured git protocol
! Authentication credentials saved in plain text
✓ Logged in as YeshwanthKumarN
-----------------------------------------------------------------------------
`unset GITHUB_TOKEN && gh auth login -h github.com -p https -s delete_repo -w`
-----------------------------------------------------------------------------

Installing Terraform Ref: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Fundamentals: All terraform does is orchestrate and manage resources through their APIs, for which it requires providers information. Provider is the translator between Terraform & the actual service.

Sample (GitHub) Provider: https://registry.terraform.io/providers/integrations/github/latest/docs
    Review: https://developer.hashicorp.com/terraform/language/expressions/version-constraints



   

