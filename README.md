<!-- start quote -->
💬 Quote of the Day: "The things you learn in maturity aren't simple things such as acquiring information and skills. You learn not to engage in self-destructive behavior. You learn not to burn up energy in anxiety. You discover how to manage your tensions. You learn that self-pity and resentment are among the most toxic of drugs. You find that the world loves talent but pays off on character."
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