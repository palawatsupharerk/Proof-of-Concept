# Proof of Concept on SAS Viya 3.5
## Background
- SASPy (Available for Python only)
  - https://support.sas.com/en/software/saspy.html
- SWAT (SAS Scripting Wrapper for Analytics Trasfer)
  - Python https://developer.sas.com/guides/python-swat.html
  - R https://developer.sas.com/guides/r.html
## Constraints
Due to Security Policy Enforcement, port 5570 and 8777 are prohibitive for PoC which are stardard CAS ports for SWAT connection both Binary Connection and REST Connection Directly to CAS). See also in SAS documenation at https://go.documentation.sas.com/doc/en/pgmsascdc/9.4_3.5/caspg3r/p0paczu3x2qu0wn1p94ees7y5ls8.htm?homeOnFail. Therefore, this PoC will focus on SWAT test on Client side through REST Connection with HTTP Server. SAS Viya uses an HTTP server to proxy requests to services. By default, the HTTP server is configured to use TLS port 443. 
## Python Client Computing Environment
- Python 3.8 (Anaconda) for Windows (64-bit)
- JupyterLab 3+
- swat 1.9.2
- saspy 3.7.2

## R Client Computing Environment
- R 4.1+ for Windows (64-bit) https://wwww.r-project.org/
- RStudio 1.4+ for Windows (64-bit) https://www.rstudio,com/
- swat 1.5+

## Installation
- SASPy https://sassoftware.github.io/saspy/install.html#installation
- Python swat https://sassoftware.github.io/python-swat/install.html
- R swat https://github.com/sassoftware/R-swat

## How to connect SAS Viya (SPRE=SAS Programming Runtime Environment) with SASPy
#### Assumption
   - Anaconda Python is already installed on Client computer
#### Procedures
1. Open Anaconda Prompt and Install SASPy package on Client computer while connecting to Internet without OPS VPN activation
2. Configure SASpy
3. Create Authentication file

## How to connect SAS Viya (CAS) with Python SWAT
#### Assumption
   - Anaconda Python is already installed on Client computer
#### Procedures
1. Open Anaconda Prompt and Install SWAT package
   ```
   conda install -c sasinstitute swat
   ```
3. Run SAS code to encode your password
   ```
   PROC PWENCODE IN='<your password>';
   RUN;
   ```
## How to connect SAS Viya (CAS) with R SWAT
#### Assumption
   - Both R (R Computing) and Rstudio is already installed on Client computer
#### Procedures
1. Open RStudio and Install SWAT package
   ```
   install.package('https://github.com/sassoftware/R-swat/releases/download/v1.5.0/R-swat-1.5.0-win64.tar.gz', repos=NULL, type='file')
   ```
3. Run SAS code to encode your password
   ```
   PROC PWENCODE IN='<your password>';
   RUN;
   ```

