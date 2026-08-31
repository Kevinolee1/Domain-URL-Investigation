# Domain-URL-Investigation
Built a Python tool that automatically queries VirusTotal to investigate domains and URLs, returning malicious, suspicious, harmless, and undetected results for SOC analysis
![Image alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/facd61f87fed0f3c20338600363570446c242bf8/Domain%20%26%20URL%20Investigation/Screenshot%202026-08-31%20111145.png)
![Inage alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/b5edf1f9bc7331b670fa869d8fdcf96edca25964/Domain%20%26%20URL%20Investigation/Screenshot%202026-08-31%20111217.png)
Go to Vs Code and replace the current main.py with
import os
import re
import ipaddress
import requests
import base64
from urllib.parse import urlparse
from dotenv import load_dotenv

load_dotenv()

api_key = os.getenv("VT_API_KEY")

headers = {
    "x-apikey": api_key
}


def detect_ioc_type(ioc):
    ioc = ioc.strip()

    if re.fullmatch(r"[A-Fa-f0-9]{64}", ioc):
        return "SHA-256 Hash"

    try:
        ipaddress.ip_address(ioc)
        return "IP Address"
    except ValueError:
        pass

    parsed = urlparse(ioc)
    if parsed.scheme in ("http", "https") and parsed.netloc:
        return "URL"

    domain_pattern = r"^(?:[A-Za-z0-9](?:[A-Za-z0-9-]{0,61}[A-Za-z0-9])?\.)+[A-Za-z]{2,63}$"

    if re.fullmatch(domain_pattern, ioc):
        return "Domain"

    return "Unknown"


def print_results(stats):
    print()
    print("VirusTotal Results")
    print("------------------")
    print(f"Malicious:  {stats.get('malicious', 0)}")
    print(f"Suspicious: {stats.get('suspicious', 0)}")
    print(f"Harmless:   {stats.get('harmless', 0)}")
    print(f"Undetected: {stats.get('undetected', 0)}")


def investigate_domain(domain):
    url = f"https://www.virustotal.com/api/v3/domains/{domain}"

    response = requests.get(url, headers=headers)

    if response.status_code == 200:
        data = response.json()
        stats = data["data"]["attributes"]["last_analysis_stats"]
        print_results(stats)
    else:
        print(f"Lookup failed. Status Code: {response.status_code}")
        print(response.text)


def investigate_url(target_url):
    url_id = base64.urlsafe_b64encode(
        target_url.encode()
    ).decode().strip("=")

    api_url = f"https://www.virustotal.com/api/v3/urls/{url_id}"

    response = requests.get(api_url, headers=headers)

    if response.status_code == 200:
        data = response.json()
        stats = data["data"]["attributes"]["last_analysis_stats"]
        print_results(stats)
    else:
        print(f"Lookup failed. Status Code: {response.status_code}")
        print(response.text)


ioc = input("Enter IOC to investigate: ").strip()

ioc_type = detect_ioc_type(ioc)

print()
print("SOC IOC Investigation Tool")
print("--------------------------")
print(f"IOC:  {ioc}")
print(f"Type: {ioc_type}")


if ioc_type == "Domain":
    investigate_domain(ioc)

elif ioc_type == "URL":
    investigate_url(ioc)

else:
    print()
    print("This lab currently investigates Domains and URLs only.")
    Press ctrl+s to save

Go to PowerShell to test the domain by typing python main.py and press enter
Then type example.com and press enter for enter IOC to investigate:
You should get
 
SOC IOC Investigation Tool
--------------------------
IOC:  example.com
Type: Domain

VirusTotal Results
------------------
Malicious:  0
Suspicious: 0
Harmless:   ...
Undetected: ...

Next type in type python main.py and press enter for the URL test.
then type https://example.com and press enter for Enter IOC to investigate:
You should get


SOC IOC Investigation Tool
--------------------------
IOC:  https://example.com
Type: URL

VirusTotal Results
------------------
Malicious:  0
Suspicious: 0
Harmless:   65
Undetected: 27
