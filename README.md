# tryhackme-badge-action-workflow
A github action for tryhackme to fetch and regenerate static badge image which can be used in the Readme

This is a GitHub Action that fetches your latest TryHackMe badge, downloads it, and commits it to your repository.

### Features
- Fetches the latest badge based on your TryHackMe user ID.
- Downloads the badge image to a specified file path.
- Commits the downloaded image to your repository with a custom message.
- Allows setting a custom committer username.

### Usage
- Add this script to your GitHub repository as a .yml file (e.g., update-tryhackme-badge.yml).
- Configure the action with the following inputs:
    - GITHUB_TOKEN: Your GitHub Personal Access Token (required, set as a secret).
    - image_path: The path to store the downloaded badge image (defaults to ./assets/tryhackme-badge.png).
    - username: Your TryHackMe username (defaults to the value in a secret named THM_USERNAME).
    - user_id: Your TryHackMe user ID (defaults to the value in a secret named THM_USER_ID).

```
name: Update TryHackMe Badge

on:
  schedule:
    - cron: '0 0 * * *' # Runs every day at midnight
  workflow_dispatch: # Allows manual triggering

jobs:
  update-badge:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Fetch TryHackMe Badge
      uses: DhanushNehru/tryhackme-badge-action-workflow@v1.0
      with:
        image_path: './assets/tryhackme-badge.png'
        username: 'your_tryhackme_username'
        user_id: 'your_tryhackme_user_id'
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```