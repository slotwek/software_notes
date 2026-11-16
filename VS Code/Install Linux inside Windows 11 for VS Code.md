---
date: 2026-03-30
aliases:
relates_to:
---
In command prompt write:
```cmd
$ wsl  --install
>>>
Downloading: Windows Subsystem for Linux 2.6.3
Installing: Windows Subsystem for Linux 2.6.3
Windows Subsystem for Linux 2.6.3 has been installed.
Installing Windows optional component: VirtualMachinePlatform

Deployment Image Servicing and Management tool
Version: 10.0.26100.5074

Image Version: 10.0.26200.8037

Enabling feature(s)
[==========================100.0%==========================]
The operation completed successfully.
The requested operation is successful. Changes will not be effective until the system is rebooted.
The requested operation is successful. Changes will not be effective until the system is rebooted.
PS C:\Users\slotw>
```

# Still I couldn't run the command:
```bash
PS C:\Users\slotw\Qsync\002_GitHub_repos\Build-REST-APIs-with-FastAPI> wsl bash .\Ch01\01_02\post.sh
Windows Subsystem for Linux has no installed distributions.
You can resolve this by installing a distribution with the instructions below:

Use 'wsl.exe --list --online' to list available distributions
and 'wsl.exe --install <Distro>' to install.
PS C:\Users\slotw\Qsync\002_GitHub_repos\Build-REST-APIs-with-FastAPI> wsl --list  --online
The following is a list of valid distributions that can be installed.
Install using 'wsl.exe --install <Distro>'.

NAME                            FRIENDLY NAME
Ubuntu                          Ubuntu
Ubuntu-24.04                    Ubuntu 24.04 LTS
Ubuntu-22.04                    Ubuntu 22.04 LTS
Ubuntu-20.04                    Ubuntu 20.04 LTS
openSUSE-Tumbleweed             openSUSE Tumbleweed
openSUSE-Leap-16.0              openSUSE Leap 16.0
SUSE-Linux-Enterprise-15-SP7    SUSE Linux Enterprise 15 SP7
SUSE-Linux-Enterprise-16.0      SUSE Linux Enterprise 16.0
kali-linux                      Kali Linux Rolling
Debian                          Debian GNU/Linux
AlmaLinux-8                     AlmaLinux OS 8
AlmaLinux-9                     AlmaLinux OS 9
AlmaLinux-Kitten-10             AlmaLinux OS Kitten 10
AlmaLinux-10                    AlmaLinux OS 10
archlinux                       Arch Linux
FedoraLinux-43                  Fedora Linux 43
FedoraLinux-42                  Fedora Linux 42
eLxr                            eLxr 12.12.0.0 GNU/Linux
OracleLinux_7_9                 Oracle Linux 7.9
OracleLinux_8_10                Oracle Linux 8.10
OracleLinux_9_5                 Oracle Linux 9.5
openSUSE-Leap-15.6              openSUSE Leap 15.6
SUSE-Linux-Enterprise-15-SP6    SUSE Linux Enterprise 15 SP6
PS C:\Users\slotw\Qsync\002_GitHub_repos\Build-REST-APIs-with-FastAPI> wsl --install Ubuntu
The requested operation is successful. Changes will not be effective until the system is rebooted.
PS C:\Users\slotw\Qsync\002_GitHub_repos\Build-REST-APIs-with-FastAPI>
```

# How to install ubuntu on WSL
- [Tutorial](https://www.youtube.com/watch?v=zZf4YH4WiZo)

# After installation Linux and using VS Code
- In VS Code - press `Ctrl + Shift  + P`
	- Type: `Terminal: Select Default Profile`
		- Select: **`Ubuntu (WSL)`**
- then you can run the code in VS Code
```bash
slotwek@probook:/mnt/c/Users/slotw/Qsync/002_GitHub_repos/Build-REST-APIs-with-FastAPI$ ./Ch01/01_02/post.sh 
HTTP/1.1 200 OK
Date: Sun, 29 Mar 2026 18:12:31 GMT
Content-Type: application/json
Content-Length: 504
Connection: close
Server: gunicorn/19.9.0
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true

{
  "args": {},
  "data": "{\n  \"login\": \"elliot\",\n  \"action\": \"read\",\n  \"uri\": \"file:///etc/passwd\"\n}\n",
  "files": {},
  "form": {},
  "headers": {
    "Content-Length": "75",
    "Content-Type": "application/json",
    "Host": "httpbin.org",
    "X-Amzn-Trace-Id": "Root=1-69c96b8f-7e77413d571a7b3a63c4fdc6"
  },
  "json": {
    "action": "read",
    "login": "elliot",
    "uri": "file:///etc/passwd"
  },
  "origin": "217.155.179.7",
  "url": "http://httpbin.org/post"
}
slotwek@probook:/mnt/c/Users/slotw/Qsync/002_GitHub_repos/Build-REST-APIs-with-FastAPI$
```

## This still wasn't enough to run the server!
- how to install FastAPI on wsl ubuntu
### Step 1: Update system packages and install Python essentials 
Open your WSL Ubuntu terminal and run the following commands to ensure your system is up-to-date and necessary Python tools are installed: 
```bash
sudo apt update && sudo apt upgrade -y
```
```bash
sudo apt install python3 python3-pip python3-venv python3-dev -y
```

### Step 2: Create and activate a virtual environment 
Using a virtual environment is a best practice to isolate your project's dependencies from the system's global Python packages. 
1. **Create a project directory** and navigate into it:
	```bash
	mkdir my_fastapi_project
	cd my_fastapi_project
	```
	==🟢Note, that I did this is in the main folder 023_build-rest-apis-with-fastapi==
2. **Create a virtual environment** named `venv`:
    ```bash
    python3 -m venv venv
    ```
	**Note!** This will take a while and there is nothing printed to the screen. But it is working. 
3. **Activate the virtual environment**:
    ```bash
    source venv/bin/activate
    ```
Your terminal prompt should now be prefixed with `(venv)`, indicating the environment is active. 

### Step 3: Install FastAPI and Uvicorn 
Install FastAPI and an ASGI server like Uvicorn within your activated virtual environment using `pip`. Installing with the `[standard]` extra ensures you get high-performance dependencies automatically. 
```bash
pip install "fastapi[standard]"
```
==🟢Alternatively, you can install them separately: ==
```bash
# This one didn't work for me! The one above worked!
pip install fastapi uvicorn
```
Then it failed and I had to follow it up with:
```bash
pip install "fastapi[standard]"
```

### (Optional) Step 4: Create a sample FastAPI application 
Create a file named `main.py` in your project directory and add a simple FastAPI application: 
```bash
# Create the file (you can use a text editor like nano or vim instead)
touch main.py

# Add the following code to main.py
cat <<EOF > main.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}
EOF
```
> [!multi-column] Running the server
> ```bash
> $ fastapi  run  ./Ch02/02_02/server.py
> ```
>
>> [!NOTE]- wsl output (bash output of running server)
>> 
>> ```bash
>>  FastAPI   Starting production server 🚀
>>  
>>              Searching for package file structure from directories with __init__.py files
>>              Importing from
>>              /mnt/c/Users/slotw/Qsync/002_GitHub_repos/Build-REST-APIs-with-FastAPI/Ch02/02_02
>> 
>>     module   🐍 server.py
>> 
>>       code   Importing the FastAPI app object from the module with the following code:
>> 
>>              from server import app
>> 
>>        app   Using import string: server:app
>> 
>>     server   Server started at http://0.0.0.0:8000
>>     server   Documentation at http://0.0.0.0:8000/docs
>> ```
>> 

Now, you can open web-browser with this [link](http://0.0.0.0:8000)
or paste it manually to web-browser:
```text
http://0.0.0.0:8000
```

### (Optional) Step 5: Run the FastAPI application 
- *I followed the course from here: [[023 - Build REST API with FastAPI#2.2 Running the server]]*
Start the development server using `uvicorn`. The `--reload` flag is useful for development as it automatically restarts the server when code changes. 
```bash
uvicorn main:app --reload
```

You should see output similar to this:
```bash
INFO:     Will watch for changes in these directories: [...]
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process [...] using StatReload
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

### (Optional) Step 6: Access your API
Open your web browser (on Windows) and navigate to **`http://127.0.0.1:8000`** to see the JSON response `{"Hello": "World"}`. 
You can also access the interactive API documentation (Swagger UI) at **`http://127.0.0.1:8000/docs`**.

---
[[VS Code - main]]