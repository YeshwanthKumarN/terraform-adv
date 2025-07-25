--------------------------------
Prerequisites for the Codespace
--------------------------------

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

`unset GITHUB_TOKEN && gh auth login -h github.com -p https -s delete_repo -w`


Installing Terraform Ref: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Fundamentals: All terraform does is orchestrate and manage resources through their APIs, for which it requires providers information. Provider is the translator between Terraform & the actual service.

Sample (GitHub) Provider: https://registry.terraform.io/providers/integrations/github/latest/docs
    Review: https://developer.hashicorp.com/terraform/language/expressions/version-constraints

---------------
Initialization
---------------

terraform init   >>  https://developer.hashicorp.com/terraform/cli/commands/init

@YeshwanthKumarN ➜ /workspaces/terraform-adv (main) $ terraform init
Initializing the backend...
Initializing provider plugins...
- Finding integrations/github versions matching "~> 6.0"...
- Installing integrations/github v6.6.0...
- Installed integrations/github v6.6.0 (signed by a HashiCorp partner, key ID 38027F80D7FD5FB2)
Partner and community providers are signed by their developers.
If you'd like to know more about provider signing, you can read about it here:
https://developer.hashicorp.com/terraform/cli/plugins/signing
Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

------------------
Backend
------------------

Backend are used to store state files (which is a super important feature of terraform) Ref: https://developer.hashicorp.com/terraform/language/backend

--------------
Resources
--------------

main.tf - contains the resource definitions

Terraform workflow
-----------------
Code > Plan > Apply

"Plan" Ref: https://developer.hashicorp.com/terraform/cli/commands/plan
Note: Ensure you run history -c to clear the console for sensitive information

@YeshwanthKumarN ➜ /workspaces/terraform-adv/terraform-code (main) $ terraform plan -out=plan1

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # github_repository.create-repo will be created
  + resource "github_repository" "create-repo" {
      + allow_auto_merge            = false
      + allow_merge_commit          = true
      + allow_rebase_merge          = true
      + allow_squash_merge          = true
      + archived                    = false
      + auto_init                   = true
      + default_branch              = (known after apply)
      + delete_branch_on_merge      = false
      + description                 = "Demo repo created and managed by TF"
      + etag                        = (known after apply)
      + full_name                   = (known after apply)
      + git_clone_url               = (known after apply)
      + html_url                    = (known after apply)
      + http_clone_url              = (known after apply)
      + id                          = (known after apply)
      + merge_commit_message        = "PR_TITLE"
      + merge_commit_title          = "MERGE_MESSAGE"
      + name                        = "demo-repo"
      + node_id                     = (known after apply)
      + primary_language            = (known after apply)
      + private                     = (known after apply)
      + repo_id                     = (known after apply)
      + squash_merge_commit_message = "COMMIT_MESSAGES"
      + squash_merge_commit_title   = "COMMIT_OR_PR_TITLE"
      + ssh_clone_url               = (known after apply)
      + svn_url                     = (known after apply)
      + topics                      = (known after apply)
      + visibility                  = "public"
      + web_commit_signoff_required = false

      + security_and_analysis (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Saved the plan to: plan1

To perform exactly these actions, run the following command to apply:
    terraform apply "plan1"
    
---------

"Apply" Ref: https://developer.hashicorp.com/terraform/cli/commands/apply
Note: 

@YeshwanthKumarN ➜ /workspaces/terraform-adv/terraform-code (main) $ terraform apply plan1
github_repository.create-repo: Creating...
github_repository.create-repo: Creation complete after 6s [id=demo-repo]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

--------

"Destroy" Ref: https://developer.hashicorp.com/terraform/cli/commands/destroy
Note: Destroy doesn't need a plan

@YeshwanthKumarN ➜ /workspaces/terraform-adv/terraform-code (main) $ terraform destroy
github_repository.create-repo: Refreshing state... [id=demo-repo]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # github_repository.create-repo will be destroyed
  - resource "github_repository" "create-repo" {
      - allow_auto_merge            = false -> null
      - allow_merge_commit          = true -> null
      - allow_rebase_merge          = true -> null
      - allow_squash_merge          = true -> null
      - allow_update_branch         = false -> null
      - archived                    = false -> null
      - auto_init                   = true -> null
      - default_branch              = "main" -> null
      - delete_branch_on_merge      = false -> null
      - description                 = "Demo repo created and managed by TF" -> null
      - etag                        = "W/\"bee49a57a55e823caaedf0b6af334cbc460c444c45d040c9b0b32088da169556\"" -> null
      - full_name                   = "YeshwanthKumarN/demo-repo" -> null
      - git_clone_url               = "git://github.com/YeshwanthKumarN/demo-repo.git" -> null
      - has_discussions             = false -> null
      - has_downloads               = false -> null
      - has_issues                  = false -> null
      - has_projects                = false -> null
      - has_wiki                    = false -> null
      - html_url                    = "https://github.com/YeshwanthKumarN/demo-repo" -> null
      - http_clone_url              = "https://github.com/YeshwanthKumarN/demo-repo.git" -> null
      - id                          = "demo-repo" -> null
      - is_template                 = false -> null
      - merge_commit_message        = "PR_TITLE" -> null
      - merge_commit_title          = "MERGE_MESSAGE" -> null
      - name                        = "demo-repo" -> null
      - node_id                     = "R_kgDOPStCAg" -> null
      - private                     = false -> null
      - repo_id                     = 1026245122 -> null
      - squash_merge_commit_message = "COMMIT_MESSAGES" -> null
      - squash_merge_commit_title   = "COMMIT_OR_PR_TITLE" -> null
      - ssh_clone_url               = "git@github.com:YeshwanthKumarN/demo-repo.git" -> null
      - svn_url                     = "https://github.com/YeshwanthKumarN/demo-repo" -> null
      - topics                      = [] -> null
      - visibility                  = "public" -> null
      - vulnerability_alerts        = false -> null
      - web_commit_signoff_required = false -> null
        # (2 unchanged attributes hidden)

      - security_and_analysis {
          - secret_scanning {
              - status = "enabled" -> null
            }
          - secret_scanning_push_protection {
              - status = "enabled" -> null
            }
        }
    }

Plan: 0 to add, 0 to change, 1 to destroy.

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

github_repository.create-repo: Destroying... [id=demo-repo]
github_repository.create-repo: Destruction complete after 1s

Destroy complete! Resources: 1 destroyed.

   

