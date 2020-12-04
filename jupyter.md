# how set jupyter to serve on static ip [ref](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html)

## generate jupyter_notebook_cofnfig.py
cd ~  
jupyter notebook --generate-config
cd ~/.jupyter

## generate password when login jupyter lab
#### execute codes below in python interpreter
```
from IPython.lib import passwd
print(passwd("""your password"""))
# then you will receive something like
# 'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
``` 

## create self-signed certificate
openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout mykey.key -out mycert.pem  

## edit jupyter_notebook_cofnfig.py
```
# Set options for certfile, ip, password, and toggle off
# browser auto-opening
c.NotebookApp.certfile = u'/absolute/path/to/your/certificate/mycert.pem'
c.NotebookApp.keyfile = u'/absolute/path/to/your/certificate/mykey.key'
# Set ip to '*' to bind on all interfaces (ips) for the public server
c.NotebookApp.ip = '*'
c.NotebookApp.password = u'sha1:bcd259ccf...<your hashed password here>'
c.NotebookApp.open_browser = False
c.NotebookApp.allow_origin = '*'
c.NotebookApp.ip = '0.0.0.0'
```


