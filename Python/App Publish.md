## On IIS SERVER
- Navigate to folder
```sh
cd C:\inetpub\wwwroot\aw_python_ai_app
```

- Activate the virtual environment (if it exists):
```sh
.\venv\Scripts\activate
```
- Run the app
```sh
uvicorn main:app --host 0.0.0.0 --port 8000
```
## Download nssm.exe and extract below path
 - C:\nssm\nssm.exe install FastAPI

- In the GUI:

Path → C:\Users\awt-admin\AppData\Local\Programs\Python\Python39\python.exe
Startup directory → C:\inetpub\wwwroot\aw_python_ai_app
Arguments → -m uvicorn main:app --host 127.0.0.1 --port 8000

After configuration hit below command in CMD
```sh
net start FastAPI
```
Now site will be accessible at
http://127.0.0.1:8000/

