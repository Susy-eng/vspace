---
title: "Software Testing by Using Robot Framework"
date: 2024-06-27T16:38:54+08:00
draft: true
---

### Pre-requisite  
Make sure the following things is installed.
- Python
- pip
- env
- robotframework `pip3 install robotframework`  
- selenium library `pip3 install --upgrade robotframework-seleniumlibrary`  

```commandline
mkdir WebTesting
cd WebTesting
python3.12 -m venv env
source env/bin/activate
pip3 install robotframework
pip3 install --upgrade robotframework-seleniumlibrary
```
To check if selenium is installed successfully,run the following command, there will be no error.  
```commandline
python3
import selenium
```
- Pycharm IDE and Intellibot plugin
- Selenium BrowserDrivers  
You could find the packages from [here](https://www.selenium.dev/downloads/), choose one according to your system.
Take firefox for an example, you could find it [here](https://github.com/mozilla/geckodriver/releases). 
UnZip the package and put it in a specific folder.And the location to PATH.  
```commandline
PATH=/Users/susy/Desktop/testdrivers:${PATH}
export PATH
echo $PATH
```
### Start a New Project

**Step1: Create and organize your folders**  
Create New project via PyCharm IDE, choose existing interpreter.  
New folders under your project. With name Libraries, Resources, Results, Tests, TestSuite respectively.  
New subfolders of TestSuite can be FunctionalTests, AcceptanceTests, etc.  

**Step2: New robot file**  
For example Search.robot

