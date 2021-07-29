# Proof of Concept on SAS Viya 3.5
## Special Notice
This Proof of Concept (PoC) is conducted on SAS Viya 3.5, not SAS Viya 4.0 (also known as Viya 2021.x). Therefore, it is advisable to conduct PoC on SAS Viya 4.0 when it is available for evaluation purpose.
There are some features that are not available on SAS Viya 3.5 but will be available on SAS Viya 4.0, for example
- Process Flow (used for processing ad hoc data request)
## Constraints
Due to Security Policy Enforcement, port 5570 and 8777 are prohibitive for PoC which are stardard ports for SWAT connection both Binary Connection and REST Connection Directly to CAS). See also in SAS documenation at https://go.documentation.sas.com/doc/en/pgmsascdc/9.4_3.5/caspg3r/p0paczu3x2qu0wn1p94ees7y5ls8.htm?homeOnFail. Therefore, this PoC will focus on SWAT test on Client side through REST Connection with HTTP Server. SAS Viya uses an HTTP server to proxy requests to services. By default, the HTTP server is configured to use TLS port 443. 
## Python Client Computing Environment
- Python 3.8 (Anaconda) for Windows (64-bit)
- JupyterLab 3+
- swat 1.9.2
- saspy 3.7.2

## R Client Computing Environment
- R 4.1+ for Windows (64-bit)
- RStudio 1.4+ for Windows (64-bit)
- swat 1.5+

## Installation
- SASpy https://sassoftware.github.io/saspy/install.html#installation
- Python swat https://sassoftware.github.io/python-swat/install.html
- R swat https://github.com/sassoftware/R-swat
