# K8s_Certificates

### Create a Key and CSR for a User

**1. To generate a key file**
```
openssl genrsa -out pavan.key 2048
```

**2. To generate a csr file**
```
openssl req -new -key pavan.key -out pavan.csr -subj "/CN=pavan"
```

**3. Create a CSR YAML as `csr.yaml`**

**4. Copy the pavan.csr request in the `csr.yaml` but use the below to encode in a single line**
```
cat pavan.csr | base64 | tr -d "\n"
```

**5. Apply the `csr.yaml` to the Cluster**
```
k apply -f csr.yaml
```

**6. Check for the CSR created**
```
k get csr
```
![image](https://github.com/user-attachments/assets/ecf627a8-243a-40e9-ab0e-615e3b09ceaa)

(Shows as Pending as you have not approved it)

```
`k describe csr pavan`
```
![image](https://github.com/user-attachments/assets/adde8245-5d76-4ab6-86c0-dfef9986d66f)

(Here also you can see as Pending)

**7. To approve a csr**
```
k certificate approve pavan
```
```
k describe csr pavan
```
![image](https://github.com/user-attachments/assets/fa3baa79-b5ce-4184-ba27-599c31f3712f)

(Now you can see its Approved)

**8. If, To deny a csr**
```
k certificate deny pavan
```

**9. Now the CSR is approved and we have to share this with the user**
```
k get csr pavan -o yaml > issuecert.yaml
```

**10. Copy the certificate and decode it using the below**
```
echo <certificate> | base64 -d
```
![image](https://github.com/user-attachments/assets/64f4b248-c5f5-413f-a06c-b50002abb500)
