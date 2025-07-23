# Identity Federation & SSO Setup

## Project Overview
This project demonstrates **Identity Federation** using **SAML, OAuth2, and OpenID Connect** with **Okta**, enabling seamless **Single Sign-On (SSO)** across multiple applications.

## Features
- **SAML-Based Identity Federation Setup**
- **OAuth2 & OpenID Connect for Cross-Domain SSO**
- **User Authentication Flow with Identity Provider (IdP)**
- **Okta Integration for Federated Authentication**

---

## Prerequisites
- [ ] Okta Developer Account ([Sign up for free](https://developer.okta.com/))
- [ ] Python 3.x installed
- [ ] SAML Service Provider (SP) Setup
- [ ] OAuth2 Client & Secret for OIDC Authentication

---

## Setup Instructions

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/yourgithubusername/identity-federation-sso.git
cd identity-federation-sso
```

### 2️⃣ Install Dependencies
```bash
pip install -r requirements.txt
```

### 3️⃣ Configure Environment Variables
Create a `.env` file in the project root and add:
```
OKTA_ORG_URL=https://your-okta-domain.okta.com
SAML_SP_ENTITY_ID=your_saml_sp_entity_id
OAUTH2_CLIENT_ID=your_client_id
OAUTH2_CLIENT_SECRET=your_client_secret
```

### 4️⃣ Run the Federation & SSO Setup
```bash
python setup_federation.py
```

---

## Example Code

### Setting Up a SAML Authentication Request
```python
import requests
import os

OKTA_ORG_URL = os.getenv("OKTA_ORG_URL")
SAML_SP_ENTITY_ID = os.getenv("SAML_SP_ENTITY_ID")

saml_request = {
    "entityId": SAML_SP_ENTITY_ID,
    "acsUrl": f"{OKTA_ORG_URL}/sso/saml",
    "nameIdFormat": "urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"
}

response = requests.post(f"{OKTA_ORG_URL}/api/v1/authn", json=saml_request)
print(response.json())
```

### Performing OAuth2 Authentication
```python
import requests
import os

OKTA_ORG_URL = os.getenv("OKTA_ORG_URL")
OAUTH2_CLIENT_ID = os.getenv("OAUTH2_CLIENT_ID")
OAUTH2_CLIENT_SECRET = os.getenv("OAUTH2_CLIENT_SECRET")

def get_oauth2_token():
    data = {
        "grant_type": "client_credentials",
        "client_id": OAUTH2_CLIENT_ID,
        "client_secret": OAUTH2_CLIENT_SECRET,
        "scope": "openid profile email"
    }
    response = requests.post(f"{OKTA_ORG_URL}/oauth2/v1/token", data=data)
    return response.json()

print(get_oauth2_token())
```

---


 
 
 
