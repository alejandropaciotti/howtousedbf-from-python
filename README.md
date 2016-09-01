How to make a rest service from a dbf with python

```sql
#
# VISUAL FOX PRO - CODE
#
DEFINE CLASS Testing AS CUSTOM OLEPUBLIC

    PROCEDURE INIT
        ON ERROR
        SET CONSOLE OFF
        SET NOTIFY OFF
        SET SAFETY OFF
        SET TALK OFF
        SET NOTIFY OFF
    ENDPROC

    FUNCTION get_input_out(input AS STRING) AS STRING
        output = input
        RETURN output
    ENDFUNC

ENDDEFINE
```

```sql
# Instructions: Build the project as single-threaded COM
# Register the library with:
```

```shell
C:/windows/system32/regsvr32.exe [pathToDLL-file]
```

```sql
# Use with (for test)

o = CREATEOBJECTEX("expose-dll.Testing")
? o.get_input_out("Any string")
```

###### INSTALL PYTHON 2.7

http://docs.python-guide.org/en/latest/starting/install/win/

(add C:/Python27 to the PATH enviromental variable and C:/Python27/Scripts)

##### Download the pywin32-220.win32-py2.7.exe from and install it:
https://sourceforge.net/projects/pywin32/files/pywin32/Build%20220/


#### TEST PYTHON LYBRARY

```python
from win32com.client import Dispatch
oFox = Dispatch("expose-dll.Testing")
# where the file name compiled by VFP is com.dll and the olepublic class is testing.
# in Windows this stuff is not case sensitive.
print oFox.get_input_out("something")
# to close things down..
oFox = None

```


#### INSTALL flask

```shell
pip install flask
```

###### Test de flask and python installation
Create a server.py file and copy:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/', methods=['GET'])
def root():
    return 'HELLO WORLD'

if __name__ == '__main__'    :
    app.run(host='0.0.0.0', debug=True, port=8080)
```


```shell
python server.py
```

Open the browser and navigate to http://localhost:8080


#### TEST ALL TOGETHER
```shell
from win32com.client import Dispatch
from flask import Flask
oFox = Dispatch("expose-dll.Testing")

app = Flask(__name__)

@app.route('/', methods=['GET'])
def root():
    return oFox.get_input_out("HELLO WORLD BY PASS VISUAL FOX PRO!")

if __name__ == '__main__'    :
    app.run(host='0.0.0.0', debug=True, port=8080)
```
