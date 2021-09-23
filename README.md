<!-- start quote -->
💬 Quote of the Day: "A master in the art of living draws no sharp distinction between his work and his play; his labor and his leisure; his mind and his body; his education & his recreation. He hardly knows which is which. He simply pursues his vision of excellence through whatever he is doing, and leaves others to determine whether he is working or playing. To himself, he always appears to be doing both."
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