# Domain-URL-Investigation
Built a Python tool that automatically queries VirusTotal to investigate domains and URLs, returning malicious, suspicious, harmless, and undetected results for SOC analysis
![Image alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/facd61f87fed0f3c20338600363570446c242bf8/Domain%20%26%20URL%20Investigation/Screenshot%202026-08-31%20111145.png)
![Inage alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/b5edf1f9bc7331b670fa869d8fdcf96edca25964/Domain%20%26%20URL%20Investigation/Screenshot%202026-08-31%20111217.png)
![Image alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/269374276c68767aedd4ef7d1dc84edcbfb5b8d5/Domain%20%26%20URL%20Investigation/Screenshot%202026-08-31%20111244.png)
![Image alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/d749457c3fa45d28031a0d069c53be43500e5948/Domain%20%26%20URL%20Investigation/Screenshot%202026-08-31%20111313.png)

Go to Vs Code and replace the current main.py with

![Image alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/36bd8d656959eecb62262eafe8bb2a51d416bb97/Screenshot%202026-08-31%20185743.png)
![Image alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/2cfea15f71128c45f31f141b06dacfabdf585164/Screenshot%202026-08-31%20185720.png)
![Image alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/297328c75392a983368ceb089a012a57d406b960/Domain%20%26%20URL%20Investigation/Screenshot%202026-08-31%20111725.png)
Go to PowerShell to test the domain by typing python main.py and press enter
Then type example.com and press enter for enter IOC to investigate:
You should get something like
 
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
![Image alt](https://github.com/Kevinolee1/Domain-URL-Investigation/blob/7f551502f3d6623bb3f7bf9dd6bbfb8169afd3b7/Domain%20%26%20URL%20Investigation/Screenshot%202026-08-31%20111828.png)
Next type in type python main.py and press enter for the URL test.
then type https://example.com and press enter for Enter IOC to investigate:
You should get something like


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
