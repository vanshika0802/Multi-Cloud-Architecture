# Multi-Cloud-Architecture
#aws_app
#app.py 
from flask import Flask, jsonify, render_template
import requests

app = Flask(__name__)

@app.route('/')
def home():
    # Call the GCP app
    gcp_response = requests.get('http://127.0.0.1:5001/api')  # GCP API route
    gcp_data = gcp_response.json()

    aws_message = {'message': 'Hello from AWS App!'}

    # Render index.html with both messages
    return render_template('index.html', gcp_response=gcp_data, aws_response=aws_message)

@app.route('/api')
def api():
    return jsonify({'message': 'Hello from AWS App!'})

if __name__ == '__main__':
    app.run(port=5000)

#index.html
<!DOCTYPE html>
<html>
<head>
    <title>AWS-GCP Integration</title>
</head>
<body>
    <h1>AWS-GCP Integration Page</h1>
    <p><strong>AWS Response:</strong> {{ aws_response.message }}</p>
    <p><strong>GCP Response:</strong> {{ gcp_response.message }}</p>
</body>
</html>

#gcp_app
#app.py
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/')
def home():
    return "<h2>Welcome to the GCP App</h2>"

@app.route('/api')
def api():
    return jsonify({'message': 'Hello from GCP App!'})

if __name__ == '__main__':
    app.run(port=5001)

#output
AWS-GCP Integration Page

AWS Response: Hello from AWS App!
GCP Response: Hello from GCP App!

#Documentation 
# Interoperability Demo: AWS and GCP

## 🚀 Project Overview

This project demonstrates **interoperability between two major cloud platforms: AWS and GCP**. The same Python Flask-based web application is hosted and run independently on both platforms, proving that cloud applications can seamlessly operate across environments with minimal changes.

---

## 🔧 Technologies Used

- **Python Flask** – For backend server
- **HTML/CSS** – For frontend user interface
- **AWS EC2** – For deploying the web app
- **Google Cloud Platform (GCP) Compute Engine** – For deploying the web app
- **GitHub** – For version control and source code hosting

---




