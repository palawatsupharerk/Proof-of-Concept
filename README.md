# Proof of Concept on SAS Viya 3.5
_Author: Palawat Supharerk_
## Walkthrough for Client R/Python connection to SAS Viya
- SASPy (Available for Python only) for SPRE engine and SAS 9.4
  - https://support.sas.com/en/software/saspy.html
- SWAT (SAS Scripting Wrapper for Analytics Transfer) for CAS engine
  - Python https://developer.sas.com/guides/python-swat.html
  - R https://developer.sas.com/guides/r.html
## Constraints
Due to Security Policy Enforcement, port 5570 and 8777 are prohibitive for PoC which are stardard CAS ports for SWAT connection both Binary Connection and REST Connection Directly to CAS). See also in SAS documenation at https://go.documentation.sas.com/doc/en/pgmsascdc/9.4_3.5/caspg3r/p0paczu3x2qu0wn1p94ees7y5ls8.htm?homeOnFail. Therefore, this PoC will focus on SWAT test on Client side through REST Connection with HTTP Server. SAS Viya uses an HTTP server to proxy requests to services. By default, the HTTP server is configured to use TLS port 443. 
## Python Client Computing Environment
- Python 3.8+ (Anaconda) for Windows (64-bit)
- JupyterLab 3+
- swat 1.9.2
- saspy 3.7.3

## R Client Computing Environment
- R 4.1+ for Windows (64-bit) https://www.r-project.org
- RStudio 1.4+ for Windows (64-bit) https://www.rstudio.com
- swat 1.5+

## Installation
- SASPy https://sassoftware.github.io/saspy/install.html#installation
- Python swat https://sassoftware.github.io/python-swat/install.html
- R swat https://github.com/sassoftware/R-swat

## Scenario 1: How to connect SAS Viya (SPRE=SAS Programming Runtime Environment) with SASPy
#### Assumption
   - Python (Anaconda) and JupyterLab packages are already installed on Client computer
#### Procedures
1. Open Anaconda Prompt and Install SASPy package on Client computer while connecting to Internet without VPN connection
   ```
   conda install saspy
   ```
   or if you use pip command
   ```
   pip install saspy
   ```
3. Configure SASpy

   - Goto C:\ProgramData\Anaconda3\envs\py39\Lib\site-packages\saspy\
   - copy sascfg.py to sascfg_personal.py
   - Edit sascfg_personal.py by
    
       changing
       ```
       SAS_config_names=['poc']
       ```
       appending
       ```
       poc = {'ip'      : '<SAS Viya hostname>',
              'context' : 'SAS Studio compute context',
              'authkey' : 'viyaKey',
              'encoding': 'utf-8',
              'options' : ["fullstimer", "memsize=2G"]}
       ```
4. Create Authentication file (_authinfo) in personal home folder on Client computer
   ```
   viyaKey user <your email> password <your password>
   ```
5. Make a connection to SAS Viya
   - Connect VPN
   - Start JupyterLab using Anaconda Command Prompt,
    
     for example,
     if your code located in Network S: Drive
     ```
     jupyter lab --notebook-dir S:\users\foo\bar
     ```
     if your code located in local C: drive
     ```
     jupyter lab
     ```
   - Run Python Notebook

## Scenario 2: How to connect SAS Viya (CAS) with Python SWAT
#### Assumption
   - Anaconda Python is already installed on Client computer
#### Procedures
1. Open Anaconda Prompt and Install SWAT package
   ```
   conda install -c sas-institute swat
   ```
   or if you use pip command
   ```
   pip install swat
   ```
2. Run SAS code to encode your password
   ```
   PROC PWENCODE IN='<your password>';
   RUN;
   ```
3. Make a connection to CAS server
 
## Scenario 3: How to connect SAS Viya (CAS) with R SWAT
#### Assumption
   - Both R (R Computing) and Rstudio are already installed on Client computer
#### Procedures
1. Open RStudio and Install SWAT package
   ```
   install.package('https://github.com/sassoftware/R-swat/releases/download/v1.5.0/R-swat-1.5.0-win64.tar.gz', repos=NULL, type='file')
   ```
2. Run SAS code to encode your password
   ```
   PROC PWENCODE IN='<your password>';
   RUN;
   ```
3. Make a connection to CAS server
