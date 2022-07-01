- 👋 Hi, I’m Fatima
- 🌱 I’m currently learning to code in HTML, CSS and javascript
- 🎓 I'm currently studying CS at the University of Calgary
- 📫 How to reach me; email = fatimahalani@me.com
                      phone = (587)-225-7244
                      
![](https://raw.githubusercontent.com/FatimaAlan1/github-stats/master/generated/languages.svg#gh-dark-mode-only)
name: Generate Stats Images

on:
  push:
    branches: [ master ]
  schedule:
    - cron: "5 0 * * *"
  workflow_dispatch:

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    # Check out repository under $GITHUB_WORKSPACE, so the job can access it
    - uses: actions/checkout@v2

    # Run using Python 3.8 for consistency and aiohttp
    - name: Set up Python 3.8
      uses: actions/setup-python@v2
      with:
        python-version: '3.8'
        architecture: 'x64'

    # Cache dependencies. From:
    # https://github.com/actions/cache/blob/master/examples.md#python---pip
    - uses: actions/cache@v2
      with:
        path: ~/.cache/pip
        key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
        restore-keys: |
          ${{ runner.os }}-pip-
    # Install dependencies with `pip`
    - name: Install requirements
      run: |
        python3 -m pip install --upgrade pip setuptools wheel
        python3 -m pip install -r requirements.txt
    # Generate all statistics images
    - name: Generate images
      run: |
        python3 --version
        python3 generate_images.py
      env:
        ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        EXCLUDED: ${{ secrets.EXCLUDED }}
        EXCLUDED_LANGS: ${{ secrets.EXCLUDED_LANGS }}
        EXCLUDE_FORKED_REPOS: true

    # Commit all changed files to the repository
    - name: Commit to the repo
      run: |
        git config --global user.name "jstrieb/github-stats"
        git config --global user.email "github-stats[bot]@jstrieb.github.io"
        git add .
        # Force the build to succeed, even if no files were changed
        git commit -m 'Update generated files' || true
        git push
Footer
© 2022 GitHub, Inc.
Footer navigation

    Terms
    Privacy
    Security
    Status
    Docs
    Contact GitHub
    Pricing
    API
    Training
    Blog
    About


<!---
fatimaAhmed36/fatimaAhmed36 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
![](https://raw.githubusercontent.com/fatimaalan1/github-stats/master/generated/overview.svg#gh-dark-mode-only)

