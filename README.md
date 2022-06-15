## DEVWKS-2919 <br /> Real-World API Attacks, and How to Protect Your Cloud-Native Apps 

### Lab Environment: <a target="_blank" href="https://developer.cisco.com/learningcenter/labs/kubernetes-istio-sockshop-apiclarity/" rel="noopener noreferrer">APIClarity Learning Lab</a>
> **Right-click and open in a new INCOGNITO MODE/PRIVATE WINDOW**

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

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173617494-5972450c-deea-4ddb-825c-2855643d1e60.png">

1. Click on API Inventory to view the identified API calls from your environment.
2. Choose **catalogue.sock-shop** API.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173617777-652a5141-4942-47fb-a1cc-9ef2a383098e.png">

3. Choose **Reconstructed** and **Review reconstructed spec**

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173617998-b48a45e7-78f6-4f9a-b707-80763cc7f2d8.png">

4. Choose "Select All" and the **Approve review**.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173618173-ea0f0ae3-f792-43df-a9e4-4b031d696b7c.png">

5. Open the reconstructed spec in a Swagger interface using **see on Swagger**.

* Upload the captured API spec

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173618435-4e07172f-bdfd-48ae-85d1-c3f29c3a841a.png">

6. Right-click on the OpenAPI Spec in .json format and choose **Save Link As...**

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173619259-cdad0465-70dc-48a6-b6cc-1429ce3476de.png">

7. Return to the API Inventory page and choose **Provided** for the catalogue.sock-shop API.  Drag the downloaded file (or choose it from the Downlaods folder) and select **Finish**.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173619560-edd3d8e9-59b0-42eb-b0d1-474a8706d2f9.png">

8. Click back on the API Inventory button to verify that the spec for catalogue has been provided.
> This will act as the "approved" spec and revisiting the Sock Shop website and selecting different options will show variations to the provided spec.

* Observe deviations from API spec

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173624730-64135cb0-51db-4907-a5c8-e8ae22bc1b2b.png">

9. Click on API Events. This will list all of the identified API calls and note those calls that differ from the uploaded specs.

## Simulating alerts using a shell script

**Run the following commands in your terminal IN THE LEARNING LAB ENVIRONMENT**

1. Expose the telemetry port of APIClarity

```console
nohup kubectl port-forward -n apiclarity svc/apiclarity-apiclarity 9000:9000 > ~/.apiclarity.log 2>&1 &
```

2. Pull down shell script from this repo into your environment.

```console
wget https://raw.githubusercontent.com/briansak/clus2022-devwks-2919/main/alert_gen.sh
```

3. Make the shell script executable

```console
chmod +x alert_gen.sh
```

4. Exectue the shell script
```console
./alert_gen.sh
```

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173706990-cc181b5b-ad56-446b-be88-fa7deb1adcef.png">

1. Click on API Events and observe the new alerts associated with the traffic that we generated in the environment.

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/10421515/173626449-cd6dbae7-39b2-4d5d-8ab8-b66017ef4deb.png">

2. Click on **Trace Analyis** on one of the alerted events.  Observe the specific alert level and alert details.

## BONUS: Testing security using ZAP Proxy

**Run the following commands in your terminal IN THE LEARNING LAB ENVIRONMENT**


1. Download and install ZAP Proxy

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

2. **Press Enter** (repeatedly)

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

3. **Press 1**

> Which type of installation should be performed?
> Select the type of installation that you want to perform. Click Next when
> you are ready to continue.
> Standard installation [1, Enter], Custom installation [2]

4. **Press 1**

5. Exectue ZAP Proxy in daemon mode and run the initial scan.

```console
zap.sh -daemon -quickurl http://$NODE_IP:$NODE_PORT/customers -quickprogress -host localhost -port 8999 &
 ```
