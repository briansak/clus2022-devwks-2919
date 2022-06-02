## DEVWKS-3140 <br /> Real-World API Attacks, and How to Protect Your Cloud-Native Apps 

### Lab Environment: https://developer.cisco.com/learningcenter/labs/kubernetes-istio-sockshop-apiclarity/

<img width="1398" alt="image" src="https://user-images.githubusercontent.com/10421515/168375389-dd20f442-7291-48ff-b4b7-77d849b7976d.png">

### Your Lab Interface
- - - 

<img width="1398" alt="image" src="https://user-images.githubusercontent.com/10421515/168376000-1b728306-7a1b-4ba8-98b4-fa564c170178.png">


Sock Shop OpenAPI Spec:
https://microservices-demo.github.io/api/index.html

```console
apk add openjdk11
wget https://github.com/zaproxy/zaproxy/releases/download/v2.11.1/ZAP_2_11_1_unix.sh
sh ZAP_2_11_1_unix.sh
```

> Starting Installer ...
> This will install OWASP Zed Attack Proxy on your computer.
> OK [o, Enter], Cancel [c]

**Press Enter**

> Click Next to continue, or Cancel to exit Setup.
> Please read the following License Agreement. You must accept the terms of
> this agreement before continuing with the installation.
> 
> Apache License
> Version 2.0, January 2004
> http://www.apache.org/licenses/
> 
> TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION
> 
> ...
> 
> [Enter]
> 
> I accept the agreement
> Yes [1], No [2]

**Press 1**

```console
zap.sh -daemon -quickurl http://localhost:8000 -quickprogress
```


