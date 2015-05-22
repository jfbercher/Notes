These notes are the commands I used to install the [RKernel](https://github.com/IRkernel/IRkernel)
in IPython 3.1 (Jupyter), under debian Jessie. -- may 22, 2015


## Install everyting into a virtual environment (optional)

```bash
virtualenv -p python3 --system-site-packages ipython31 #create a new env
source ipython31/bin/activate # activate the env (use bash)
pip3 install ipython --upgrade  # install ipython in the new env
#also add
pip3 install tornado --upgrade
pip3 install jsonschema
```


## At the command prompt, and as root 
[eg `su` or `sudo su`]
Install required librairies/dependencies for compilation 

```bash
apt-get install libxml2-dev
apt-get install libcurl4-openssl-dev
apt-get install libssl-dev
```


## Start a R session and run:

```bash
install.packages('devtools')
# Need RCurl for install_github
install.packages('RCurl')
library(devtools)
# Install the packages
install_github('IRkernel/repr')
install_github('IRkernel/IRdisplay')
install_github('IRkernel/IRkernel')
# Install the kernel spec
IRkernel::installspec()

# At this point something fails in the installspec(). 
# you will need to run (still at R prompt)
print(system.file("kernelspec", package = "IRkernel"))

# in my case, the output was
[1] "/usr/local/lib/R/site-library/IRkernel/kernelspec"
```


## At the command prompt

- run the command (replacing /usr/.../kernelspec by the path you got just above)
```bash
ipython kernelspec install --replace --name ir --user  /usr/local/lib/R/site-library/IRkernel/kernelspec
```


## And voila

```bash
ipython3 notebook
```

--> you should get a R kernel in Jupyter's dashboard "new"dropdown menu. 