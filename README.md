<!-- start quote -->

💬 Quote of the Day: Football is a team sport, and there is no one individual who is bigger than the next person.

<!-- end quote -->

# Quote Of the Day GitHub action

This action updates a README.md file with a quote from the [Quote REST API](https://quotes.rest/).

## Inputs

| Name        | Description                                                                 | Required? |
| ----------- | ------------------------------------------------- | --------- |
| category    | Quote category to fetch. Default is 'inspire'. Other possible values: management, sports, life, funny, love, art, students | No        |
| readme_path | Path of the readme file to update. Default is './README.md'.                                                            | No        |

## Example usage

1. Add the following lines in the file where quote will be updated.
```
<!-- start quote -->

<!-- end quote -->
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
    - name: Run QOTD
      uses: victoria-lo/qotd-github-action@master
      with:
         category: 'sports'
    - name: Commit and push update
      run: |-
        git config --global user.email "qotd@action.com"
        git config --global user.name "Quote-Bot"
        git add -A
        git commit -m "Update README content"
        git push
```