# QubeDocs
Documentation Site for QubeCL

## Tutorial for Site Editors:

[General Tutorial on Markdown and MKDocs](https://ppqsense.github.io/QubeDocs/tutorial/tutorial.html)

## Previewing Site Locally

1. Create a local copy of the project repository
- Make sure that your github account is approved to access the repo and your computer has a [valid SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) associated with your github account.
- Make sure git is installed: (run `git --version` to check)
    - If not installed, download https://gitforwindows.org/ (windows)
      - or run `sudo apt install git` (Ubuntu)
    - It's fine to install with default settings (however, changing default branch name from `master` to `main` is recommended)
- From Github repo:
    - Navigate to folder of choice and select [<>**CODE**] button and copy SSH option repo path (or https path if you do not plan to push)
        - ex: `git@github.com:ppqSense/QubeDocs.git`
- On your machine, navigate to terminal
    - `cd` into folder where you wish to save the project
    - enter: `git clone <repo path>`
    - if you have error in the clone process, follow any suggested actions involving fetching or pulling (do not push to main branch)
    - P.S.  If you plan on making changes to the repo, please make sure to create a new branch and make edits to said branch; **do not push directly to main.**
1. Setup your Python Virtual Environment (**Not required for Codespace devcontainer**)
    - check to see if you have python installed with `python --version`
    - If not, install Python version 3.10+
        - Download Python for your OS: https://www.python.org/downloads/windows/
            - Check Admin privilages and add to Path options when installing (this will allow you to execute Python from command line)
            - Disable path length limit
        - Restart terminal and navigate back to project directory (rerun `python --version` to confirm installation)
    - Navigate to just above git repo project folder
    - Create a [virtual environment](https://docs.python.org/3/library/venv.html) where you will install all project dependencies
        - `python -m venv venv` (wait for operation to finish - might take a few seconds)
        - Now your directory should look like this:
            - `/QubeDocs /venv`
    - Activate virtual environment:
      - On Windows:
        - Enter `.\venv\Scripts\Activate.ps1`
            - (if you get a script execution error, you may need to open PowerShell as administrator and update the ExecutionPolicy) - [see guide here](https://lazyadmin.nl/powershell/running-scripts-is-disabled-on-this-system/)
      - On Linux: 
          - Enter ` source venv/bin/activate`
    - Your command line should now look something like this:
    `(venv) PS C:\Users\UserName\Documents\QubeDocs>`
    - the `(venv)` lets you know you are now in the virtual environment, any python packages you install from here will be associated with this environment.
2. Install Project requirements:
    - `cd` into Project folder `./QubeDocs`
    - run `pip install -r requirements.txt` to install all the Python packages required to run the project
3. Build project by running `mkdocs build`
    - Note: This will only work with virtual environment script running
4. Preview Site by running a local instance: `mkdocs serve`


Notes:

- To enable virtual environment: `.\venv\Scripts\Activate.ps1` or ` source venv/bin/activate`
- To disable, simply enter `deactivate` into terminal
- If you want to make and save edits without pushing to the site, please navigate to Github and create a new branch from main.

### How to

- Preview a specific remote branch
    - Fetch all remote branches `git fetch origin`
    - View available remote branches `git branch -r`
    - Preview specific branch `git checkout <branch-name>` (hint: use tab completion if available)
- Issues syncing?
   If you haven't made any intentional changes to the local version of the repo, then do the following before fetching:
  - `git restore .` (run in highest level folder) 
      - this should revert local changes to origin branch version, allowing you to switch branch without unsaved change errors
