# Deploy ODOO 18 Locally

In this article, I will explain how to install the community version "ODOO 18". ODOO is a very powerful ERP that brings together several modules allowing you to accomplish a great list of things such as:

- Create websites
- Create e-commerce sites
- Manage and send newsletters
- Centralize the management of your social media posts
- Manage the lifecycle of your business opportunities thanks to a CRM
- Manage your inventory
- Invoice your clients

I'll stop here because explaining all the amazing things this software can do would require a completely dedicated article.

## Prerequisites

- PyCharm installation
- Python installation
- Postgres Pg Admin

## Installation

First, you need to open your terminal and create a folder for our project that we will name `odoo-18-tuto`:

```bash
mkdir odoo-18-tuto
cd odoo-18-tuto
```

Next, we will clone the Odoo 18 community version:

```bash
git clone https://github.com/odoo/odoo.git --depth 1 --branch 18.0
```

You need to create a virtual environment with Python version 3.10 or 3.11:

```bash
python3.10 -m venv venv
```

Then, you need to create a folder that you will name `conf`:

```bash
mkdir conf
cd conf
touch odoo.conf
```

In this `odoo.conf` file, you need to copy the following connection parameters to your local Postgres database:

```ini
[options]
admin_passwd = admin123
db_maxconn = 64
db_host = localhost
db_port = 5432
db_user = odoo_user
db_password = admin
http_port = 8069
limit_memory_hard = 0
addons_path = (absolute path of addons folder) Ex: /Users/yourname/Desktop/dev/ODOO/odoo-18-tuto/odoo/addons
```

## PyCharm Configuration

1. Launch PyCharm
2. Open your "ODOO-18-TUTO" folder
3. Wait for indexing to complete (blue progress bar at the bottom right)
4. At the top, next to the play button, click on "Edit Configurations"
5. Choose a name for the configuration: `Odoo18_Tuto`

### Field Configuration

- **First field "Run"**: Absolute path of your Python version in your virtual environment
  - Example: `/Users/yourname/Desktop/dev/ODOO/odoo-18/venv/bin/python`

- **Second field "Script"**: Absolute path of the `odoo-bin` file in the odoo project
  - Example: `/Users/yourname/Desktop/dev/ODOO/odoo-18/odoo/odoo-bin`

- **Third field "Parameters"**: Add the following line:
  ```
  -c conf/odoo.conf -i base
  ```

- **Fourth field "Working directory"**: Absolute path of your odoo project
  - Example: `/Users/yourname/Desktop/dev/ODOO/odoo-18`

- **Fifth field "Environment variables"**:
  ```
  PYTHONUNBUFFERED=1
  ```

## requirements.txt Configuration

Now, we will go to the `requirements.txt` file and comment out each line that is not compatible with our Python 3.10 version.

Here is an example configuration for Python 3.10:

```txt
# The officially supported versions of the following packages are their
# python3-* equivalent distributed in Ubuntu 24.04 and Debian 12
asn1crypto==1.4.0 ; python_version < '3.11'
#asn1crypto==1.5.1 ; python_version >= '3.11'
Babel==2.9.1 ; python_version < '3.11'  # min version = 2.6.0 (Focal with security backports)
#Babel==2.10.3 ; python_version >= '3.11'
cbor2==5.4.2 ; python_version < '3.12'
#cbor2==5.6.2 ; python_version >= '3.12'
chardet==4.0.0 ; python_version < '3.11'  # (Jammy)
#chardet==5.2.0 ; python_version >= '3.11'
cryptography==3.4.8; python_version < '3.12'  # incompatibility between pyopenssl 19.0.0 and cryptography>=37.0.0
#cryptography==42.0.8 ; python_version >= '3.12'  # (Noble) min 41.0.7, pinning 42.0.8 for security fixes
decorator==4.4.2  ; python_version < '3.11'  # (Jammy)
#decorator==5.1.1  ; python_version >= '3.11'
docutils==0.17 ; python_version < '3.11'  # (Jammy)
#docutils==0.20.1 ; python_version >= '3.11'
freezegun==1.1.0 ; python_version < '3.11'  # (Jammy)
#freezegun==1.2.1 ; python_version >= '3.11'
geoip2==2.9.0
#gevent==21.8.0 ; sys_platform != 'win32' and python_version == '3.10'  # (Jammy)
gevent==22.10.2; sys_platform != 'win32' and python_version > '3.10' and python_version < '3.12'
#gevent==24.2.1 ; sys_platform != 'win32' and python_version >= '3.12'  # (Noble)
#greenlet==1.1.2 ; sys_platform != 'win32' and python_version == '3.10'  # (Jammy)
greenlet==2.0.2 ; sys_platform != 'win32' and python_version > '3.10' and python_version < '3.12'
#greenlet==3.0.3 ; sys_platform != 'win32' and python_version >= '3.12'  # (Noble)
idna==2.10 ; python_version < '3.12'  # requests 2.25.1 depends on idna<3 and >=2.5
#idna==3.6 ; python_version >= '3.12'
#Jinja2==3.0.3 ; python_version <= '3.10'
Jinja2==3.1.2 ; python_version > '3.10'
libsass==0.20.1 ; python_version < '3.11'
#libsass==0.22.0 ; python_version >= '3.11'  # (Noble) Mostly to have a wheel package
#lxml==4.8.0 ; python_version <= '3.10'
lxml==4.9.3 ; python_version > '3.10' and python_version < '3.12' # min 4.9.2, pinning 4.9.3 because of missing wheels for darwin in 4.9.3
#lxml==5.2.1; python_version >= '3.12' # (Noble - removed html clean)
#lxml-html-clean; python_version >= '3.12' # (Noble - removed from lxml, unpinned for futur security patches)
#MarkupSafe==2.0.1 ; python_version <= '3.10'
MarkupSafe==2.1.2 ; python_version > '3.10' and python_version < '3.12'
#MarkupSafe==2.1.5 ; python_version >= '3.12'  # (Noble) Mostly to have a wheel package
num2words==0.5.10 ; python_version < '3.12'  # (Jammy / Bookworm)
#num2words==0.5.13 ; python_version >= '3.12'
ofxparse==0.21
openpyxl==3.0.9 ; python_version < '3.12'
#openpyxl==3.1.2 ; python_version >= '3.12'
passlib==1.7.4 # min version = 1.7.2 (Focal with security backports)
#Pillow==9.0.1 ; python_version <= '3.10'
Pillow==9.4.0 ; python_version > '3.10' and python_version < '3.12'
#Pillow==10.2.0 ; python_version >= '3.12'  # (Noble) Mostly to have a wheel package
polib==1.1.1
#psutil==5.9.0 ; python_version <= '3.10'
psutil==5.9.4 ; python_version > '3.10' and python_version < '3.12'
#psutil==5.9.8 ; python_version >= '3.12' # (Noble) Mostly to have a wheel package
psycopg2==2.9.2 ; python_version == '3.10' # (Jammy)
#psycopg2==2.9.5 ; python_version == '3.11'
#psycopg2==2.9.9 ; python_version >= '3.12' # (Noble) Mostly to have a wheel package
pyopenssl==21.0.0 ; python_version < '3.12'
#pyopenssl==24.1.0 ; python_version >= '3.12' # (Noble) min 23.2.0, pinned for compatibility with cryptography==42.0.8 and security patches
#PyPDF2==1.26.0 ; python_version <= '3.10'
PyPDF2==2.12.1 ; python_version > '3.10'
pypiwin32 ; sys_platform == 'win32'
pyserial==3.5
python-dateutil==2.8.1 ; python_version < '3.11'
#python-dateutil==2.8.2 ; python_version >= '3.11'
python-ldap==3.4.0 ; sys_platform != 'win32' and python_version < '3.12' # min version = 3.2.0 (Focal with security backports)
#python-ldap==3.4.4 ; sys_platform != 'win32' and python_version >= '3.12'  # (Noble) Mostly to have a wheel package
python-stdnum==1.17 ; python_version < '3.11'  # (jammy)
#python-stdnum==1.19 ; python_version >= '3.11'
pytz  # no version pinning to avoid OS perturbations
pyusb==1.2.1
qrcode==7.3.1 ; python_version < '3.11'  # (jammy)
#qrcode==7.4.2 ; python_version >= '3.11'
#reportlab==3.6.8 ; python_version <= '3.10'
reportlab==3.6.12 ; python_version > '3.10' and python_version < '3.12'
#reportlab==4.1.0 ; python_version >= '3.12' # (Noble) Mostly to have a wheel package
requests==2.25.1 ;  python_version < '3.11' # versions < 2.25 aren't compatible w/ urllib3 1.26. Bullseye = 2.25.1. min version = 2.22.0 (Focal)
#requests==2.31.0 ; python_version >= '3.11' # (Noble)
rjsmin==1.1.0 ; python_version < '3.11'  # (jammy)
#rjsmin==1.2.0 ; python_version >= '3.11'
#rl-renderPM==4.0.3 ; sys_platform == 'win32' and python_version >= '3.12'  # Needed by reportlab 4.1.0 but included in deb package
urllib3==1.26.5 ; python_version < '3.12' # indirect / min version = 1.25.8 (Focal with security backports)
#urllib3==2.0.7  ; python_version >= '3.12'  # (Noble) Compatibility with cryptography
vobject==0.9.6.1
#Werkzeug==2.0.2 ; python_version <= '3.10'
Werkzeug==2.2.2 ; python_version > '3.10' and python_version < '3.12'
#Werkzeug==3.0.1 ; python_version >= '3.12'  # (Noble) Avoid deprecation warnings
xlrd==1.2.0 ; python_version < '3.12'  # (jammy)
#xlrd==2.0.1 ; python_version >= '3.12'
XlsxWriter==3.0.2 ; python_version < '3.12'  # (jammy)
#XlsxWriter==3.1.9 ; python_version >= '3.12'
xlwt==1.3.0
zeep==4.1.0 ; python_version < '3.11'  # (jammy)
#zeep==4.2.1 ; python_version >= '3.11'
```

Then, we will activate our virtual environment and install all dependencies:

```bash
source venv/bin/activate
pip install -r odoo/requirements.txt
```

**Attention**: Make sure to check in Python Package as some dependencies may be missing.

## Postgres Database Configuration

Now, you need to create your user in the database.

### Create Group Role

- **Name**: `odoo_user`
- **Password**: `admin`
- **Privileges**: Select all

That's it!

## Launching the Application

Now, press the play button to launch the application.

## Common Issues

You may encounter the following two problems:

### 1. Missing Libraries

You need to add them manually in "Python Package" by selecting the version mentioned in `requirements.txt`.

### 2. The odoo.conf File is Not Recognized

I recommend:
- Deleting the folder and its contents
- Recreating the `conf` folder + `odoo.conf` file
- Clearing PyCharm's cache

## Application Access

The application is available at the following URL once you have everything perfectly configured:

**http://localhost:8069/**
