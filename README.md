# codespaces
https://miniature-space-potato-q77pvvvr4jw93x7g4-5000.app.github.dev/htop


from flask import Flask
import subprocess
import os
from datetime import datetime
import pytz

app = Flask(__name__)

@app.route('/htop')
def htop():
    full_name = "Supriya [Your Last Name]"
    username = os.getenv("USER", os.getenv("USERNAME", "Unknown"))
    ist = pytz.timezone('Asia/Kolkata')
    server_time = datetime.now(ist).strftime('%Y-%m-%d %H:%M:%S.%f')
    top_output = subprocess.getoutput("top -b -n 1")

    response = f"""
    <pre>
    Name: {full_name}
    User: {username}
    Server Time (IST): {server_time}

    TOP output:
    {top_output}
    </pre>
    """
    return response

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
