#### WARNING: There was an error checking the latest version of pip.

```shell
(base)  ~/workspace/Python $ pip install --upgrade pip

```

#### Upgrade PIP

```shell
# if you have pip already installed
pip install --upgrade pip

# if your pip is aliased as pip3 (Python 3)
pip3 install --upgrade pip

#  if you don't have pip in your PATH environment variable
python -m pip install --upgrade pip

#  if you don't have pip in your PATH environment variable
python3 -m pip install --upgrade pip

#  if you have easy_install
easy_install --upgrade pip

#  if you get a permissions error
sudo easy_install --upgrade pip

#  if you get a permissions error when upgrading pip
pip install --upgrade pip --user

#  upgrade pip scoped to the current user (if you get permissions error)
python -m pip install --user --upgrade pip
python3 -m pip install --user --upgrade pip

#  Installing directly from get-pip.py (MacOS and Linux)
curl https://bootstrap.pypa.io/get-pip.py | python

#  if you get permissions issues
curl https://bootstrap.pypa.io/get-pip.py | sudo python

#  alternative for Ubuntu/Debian
sudo apt-get update && apt-get upgrade python-pip

#  alternative for Red Hat / CentOS / Fedora
sudo yum install epel-release
sudo yum install python-pip
sudo yum update python-pip

```

