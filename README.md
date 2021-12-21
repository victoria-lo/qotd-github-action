<!-- start quote -->
💬 Quote of the Day: "My father never kissed me, hugged me or told me that he loved me. As my only living parent, he became the filter through which I saw myself, the possibilities for my life, the world and all men. He was a conflicted and dark filter."
<!-- end quote -->

# Quote Of the Day GitHub action

This action updates a README file with a quote from the [Quote REST API](https://quotes.rest/).

## Inputs

| Name        | Description                                                                 | Required? |
| ----------- | ------------------------------------------------- | --------- |
| category    | Quote category to fetch. Default is 'inspire'. Other possible values: management, sports, life, funny, love, art, students | No        |
| readme_path | Path of the readme file to update. Default is './README.md'.                                                            | No        |

## Example usage

1. Add the following lines in the file where quote will be updated.
```
<!-- start quote --> and <!--- end quote -->
```

2. Create a workflow

```yaml
name: Update README with QOTD

on:
  workflow_dispatch:
  schedule:
  - cron: "0 0 * * *" # triggers every midnight

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Check out repo
      uses: actions/checkout@v2
    - name: Use Node
      uses: actions/setup-node@v2
      with:
        node-version: '14.x'
    - name: Install node dependencies
      run: npm install

    - name: Run QOTD action
      uses: ./ # Uses an action in the root directory
      with:
         category: 'life'
    - name: Commit and push update
      run: |-
        git config --global user.email "qotd@action.com"
        git config --global user.name "Quote-Bot"
        git add -A
        git commit -m "Added QOTD from GitHub Actions"
        git push
```