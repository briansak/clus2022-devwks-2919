## DEVWKS-2919 <br /> Real-World API Attacks, and How to Protect Your Cloud-Native Apps 

### Lab Environment: <a target="_blank" href="https://developer.cisco.com/learningcenter/labs/kubernetes-istio-sockshop-apiclarity/" rel="noopener noreferrer">APIClarity Learning Lab</a>
> **USE INCOGNITO MODE/PRIVATE WINDOW**


<img width="1398" alt="image" src="https://user-images.githubusercontent.com/10421515/168375389-dd20f442-7291-48ff-b4b7-77d849b7976d.png">

### Your Lab Interface
- - - 

<img width="1398" alt="image" src="https://user-images.githubusercontent.com/10421515/168376000-1b728306-7a1b-4ba8-98b4-fa564c170178.png">

Sock Shop OpenAPI Spec:
https://microservices-demo.github.io/api/index.html

## Steps from the Learning Lab ##

<img width="397" alt="image" src="https://user-images.githubusercontent.com/10421515/171740656-ca3fa920-3ba2-40a6-9cab-ee10c0d88544.png">

* Bringing up K8s environment
* Bringing up the Istio service mesh

<img width="397" alt="image" src="https://user-images.githubusercontent.com/10421515/171741112-30102f2d-645a-4534-907f-27ff8e056d57.png">

* Applying Istio to K8s namespace
* Deploying Sock Shop to K8s
* Exposing the web interface for Sock Shop and APIClarity

<img width="399" alt="image" src="https://user-images.githubusercontent.com/10421515/171745987-1bb3aec5-c07c-45f9-b787-002309b4b2f2.png">

* Generate API traffic using the Sock Shop web interface
* Capture the reconstructed OpenAPI spec
* Upload the captured API spec
* Observe deviations from API spec

## BONUS: Simulating attacks using ZAP Proxy and scripting

**Run the following commands in your terminal IN THE LEARNING LAB ENVIRONMENT**

#### Expose the telemetry port of APIClarity

```console
nohup kubectl port-forward -n apiclarity svc/apiclarity-apiclarity 9000:9000 > ~/.apiclarity.log 2>&1 &
```

#### Install ZAP Proxy

```console
apk add openjdk11
```
```console
wget https://github.com/zaproxy/zaproxy/releases/download/v2.11.1/ZAP_2_11_1_unix.sh
```
```console
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

> Which type of installation should be performed?
> Select the type of installation that you want to perform. Click Next when
> you are ready to continue.
> Standard installation [1, Enter], Custom installation [2]

**Press 1**

```console
zap.sh -daemon -quickurl http://$NODE_IP:$NODE_PORT/customers -quickprogress -host localhost -port 8999
 ```


