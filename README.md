# K8s_TLS

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

**5. To approve a csr**
```
kubectl certificate approve <certificate-signing-request-name>
```

**6. To deny a csr**
```
kubectl certificate deny <certificate-signing-request-name>
```
