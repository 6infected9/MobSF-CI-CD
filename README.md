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
