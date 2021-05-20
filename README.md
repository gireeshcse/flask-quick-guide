### Creating Simple Hello World Flask Project

```
python3 -m venv venv
. /venv/bin/activate
pip install flask
pip freeze > hello_requirements.txt
```

#### Simple Hello World flask web service

```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello, World!"


if __name__ == "__main__":
    app.run(port=5000,debug=True)
```

##### Running the program

```
python hello.py
```

#### Deploying application to VPS server

* Login to SSH and Install python

* Also install our Apache(Web Server) and WSGI(Web Server Gateway Interface)

```
sudo apt-get install apache2
sudo apt-get install libapache2-mod-wsgi
```

WSGI allows apache to talk to FLASK and vice versa.

* Clone the project and create the virtual environment for the project
```
cd /var/www
git clone https://github.com/gireeshcse/flask-quick-guide.git
cd flask-quick-guide
python3 -m venv venv
```
* Activate virtual environment and Install packages/modules required for the project

```
. venv/bin/activate
pip install -r hello_requirements.txt
```

* Create WSGI file (hello.wsgi)

```
import sys
sys.path.insert(0,"/var/www/flask-quick-guide")
from hello import app as application
```

* Update hello.conf and copy to apache sites available

```
sudo cp hello.conf /etc/apache2/sites-available
```

* Enable the application

