# prime
Simple .NET Core app based workflow demo.

Cheatsheet
```yaml
name: CI

on:
  push:
    branches:
    - master
    - 'releases/**'
  pull_request:
    branches:
    - master

jobs:
  build:

    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]

    runs-on: ${{ matrix.os }}

    steps:
    - uses: actions/checkout@v1
    
    - name: Setup .NET Core
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: 3.1.100
    
    - name: Build with dotnet
      run: dotnet build prime --configuration Release
    
    - name: Test with dotnet
      run: dotnet test prime
    
```

Disable fail fast
```yaml
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
      fail-fast: false
      
```

Show contexts
```yaml
    - name: Inspect contexts
      run: |
          echo "The github context is:"
          echo "${{ toJson(github) }}"
          echo ""
          echo "The job context is:"
          echo "${{ toJson(job) }}"
          echo ""
          echo "The steps context is:"
          echo "${{ toJson(steps) }}"
          echo ""
          echo "The runner context is:"
          echo "${{ toJson(runner) }}"
          echo ""
          echo "The strategy context is:"
          echo "${{ toJson(strategy) }}"
          echo ""
          echo "The matrix context is:"
          echo "${{ toJson(matrix) }}"

```
