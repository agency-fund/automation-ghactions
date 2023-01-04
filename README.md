# automation-zapier-ghactions

## Overview

- triggering event: Any trigger in Zapier.
- resulting action: GitHub Actions workflow. *Currently just outputs a message that the workflow was triggered.*
 
## Components

- this GitHub repository

## Replicating the system

1. Create a new GitHub repository.
    1. Log into the GitHub account that you want to be the owner of the new repository.
    2. On this repository's main page, click "Use this template" to create a new repository.

2. Create a repo-specific personal access token.
    1. Go to https://github.com/settings/tokens.
    2. Click on Fine-grained tokens, then Generate new token.
        - Token name: create a name based on the new repo's name
        - Custom expiration: current maximum is one year
        - Resource owner: select the organization of the new repo
        - Repository access: select "Only select repositories" and select the new repo
        - Repository permissions: for Contents, select "Access: Read and write"
    3. Click Generate token.
    4. Click Copy to clipboard.
    5. Paste the token into a new text file and save the file with the same name as the token.

3. Create a new Zap in Zapier.
   1. Log into Zapier.
   2. Click on "+ Create Zap".
   3. Click on "2. Action".
   4. In the App event, click on "Webhooks by Zapier".
   5. Under Event, select "Custom Request" and click Continue. Replace OWNER, REPO, and TOKEN as appropriate.
      - Method: POST
      - URL: https://api.github.com/repos/OWNER/REPO/dispatches
      - Data Pass-Through?: false
      - Data: {"event_type": "webhook", "client_payload": {"feeling": "zappy"}}
      - Headers (key: value):
        - Accept: application/vnd.github+json
        - Authorization: Bearer TOKEN
        - X-GitHub-Api-Version: 2022-11-28

## Modifying a replicated system

- To change what the GH Actions workflow actually does, update the .github/workflows/ci.yaml file.
- To complete the Zap, set up the trigger and then publish the Zap.
