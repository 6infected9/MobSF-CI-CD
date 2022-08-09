# Github Code Scanning Integration

Add the following to the file ``` .github/workflows/mobsfscan_sarif.yml ```


``` name: mobsfscan sarif
on:
  push:
    branches: [ master, main ]
  pull_request:
    branches: [ master, main ]

jobs:
  mobsfscan:
    runs-on: ubuntu-latest
    name: mobsfscan code scanning
    steps:
    - name: Checkout the code
      uses: actions/checkout@v2
    - name: mobsfscan
      uses: MobSF/mobsfscan@main
      with:
        args: '. --sarif --output results.sarif || true'
    - name: Upload mobsfscan report
      uses: github/codeql-action/upload-sarif@v1
      with:
        sarif_file: results.sarif 
        

```
##Sample Screenshot of the output:


<img width="966" alt="118427198-839be300-b681-11eb-8b79-92b916ffe3ef" src="https://user-images.githubusercontent.com/73776434/183712065-2c369e63-a5ab-47f0-9b51-d4c0085bdf3f.png">
