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
