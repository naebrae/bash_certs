# Bash Certificate create example scripts.

These scripts are working examples of using openssl to create certificates with DV, OV, and EV extensions.

## 1. Make Home Lab CA

Create certificate authority certificates

```
./mkcacerts
```

Root certificate dump

```
Certificate:
      Data:
          Version: 3 (0x2)

          Issuer: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab Root
          Subject: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab Root

          X509v3 extensions:
              X509v3 Key Usage: critical
                  Digital Signature, Certificate Sign, CRL Sign
              X509v3 Basic Constraints: critical
                  CA:TRUE
              X509v3 Subject Key Identifier:
                  75:20:93:60:47:5B:CF:F4:A3:8B:78:CE:55:8A:B8:3E:24:AF:67:15
```

Intermediate certificate dump

```
Certificate:
      Data:
          Version: 3 (0x2)

          Issuer: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab Root
          Subject: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab CA

          X509v3 extensions:
              X509v3 Basic Constraints: critical
                  CA:TRUE, pathlen:0
              X509v3 Key Usage: critical
                  Digital Signature, Certificate Sign, CRL Sign
              X509v3 Extended Key Usage:
                  TLS Web Server Authentication, TLS Web Client Authentication
              X509v3 Subject Key Identifier:
                  E0:88:36:B2:A4:A3:0F:6A:89:D6:30:0E:1E:1A:B3:4A:E1:C6:85:4D
              X509v3 Authority Key Identifier:
                  75:20:93:60:47:5B:CF:F4:A3:8B:78:CE:55:8A:B8:3E:24:AF:67:15
              Authority Information Access:
                  CA Issuers - URI:http://ca.lab.home/Home_Lab_Root.crt
              X509v3 CRL Distribution Points:
                  Full Name:
                    URI:http:http://ca.lab.home/Home_Lab_Root.crl
```


## 2. Certificate examples

### 2.1 mkclcert

Create a certificate with Client extensions including a uidNumber. The key is ed25519

```
./mkclcert "/OU=Clients/UID=12345+CN=sysadmin+title=System Admin+GN=System+SN=Admin+uidNumber=1000/emailAddress=sysadmin@lab.home"
```

```
Certificate:
    Data:
        Version: 3 (0x2)

        Issuer: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab CA
        Subject: OU = Clients, SN = Admin + GN = System + CN = sysadmin + 1.3.6.1.1.1.1.0 = 1000 + title = System Admin + UID = 12345

        Subject Public Key Info:
            Public Key Algorithm: ED25519

        X509v3 extensions:
            X509v3 Authority Key Identifier:
                E0:88:36:B2:A4:A3:0F:6A:89:D6:30:0E:1E:1A:B3:4A:E1:C6:85:4D
            X509v3 Subject Key Identifier:
                F2:39:9E:72:59:97:E8:26:1C:BD:E3:61:13:FD:62:15:6F:73:81:16
            X509v3 Subject Alternative Name:
                email:sysadmin@lab.home
            X509v3 Key Usage: critical
                Digital Signature
            X509v3 Extended Key Usage:
                TLS Web Client Authentication, E-mail Protection
            X509v3 Basic Constraints: critical
                CA:FALSE
            Authority Information Access:
                CA Issuers - URI:http://ca.lab.home/Home_Lab_CA.crt
            X509v3 CRL Distribution Points:
                Full Name:
                  URI:http://ca.lab.home/Home_Lab_CA.crl
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.2.3
```

### 2.2 mkdvcert

Create a certificate with Domain Validation (DV) extensions.

```
./mkdvcert sample.lab.home 127.0.0.1
```

```
Certificate:
    Data:
        Version: 3 (0x2)

        Issuer: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab CA
        Subject: OU = Domain Control Validated, OU = homelab, CN = sample.lab.home

        X509v3 extensions:
            X509v3 Authority Key Identifier:
                E0:88:36:B2:A4:A3:0F:6A:89:D6:30:0E:1E:1A:B3:4A:E1:C6:85:4D
            X509v3 Subject Key Identifier:
                27:39:06:24:90:01:F7:21:C5:CD:15:1E:0B:CE:CF:D1:EC:36:65:E5
            X509v3 Subject Alternative Name:
                DNS:sample.lab.home, IP Address:127.0.0.1
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage:
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            Authority Information Access:
                OCSP - URI:http://ocsp.lab.home
                CA Issuers - URI:http://ca.lab.home/Home_Lab_CA.crl
            X509v3 CRL Distribution Points:
                Full Name:
                  URI:http://ca.lab.home/Home_Lab_CA.crl
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.2.1
```

### 2.3 mkdvcert2

Create a certificate with Domain Validation (DV) extensions, just slightly different method.

```
./mkdvcert2 sample.lab.home 127.0.0.1
```

```
Certificate:
    Data:
        Version: 3 (0x2)

        Issuer: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab CA
        Subject: OU = Domain Control Validated, OU = homelab, CN = sample.lab.home

        X509v3 extensions:
            X509v3 Authority Key Identifier:
                E0:88:36:B2:A4:A3:0F:6A:89:D6:30:0E:1E:1A:B3:4A:E1:C6:85:4D
            X509v3 Subject Key Identifier:
                29:B9:CE:6A:7F:36:38:0D:C1:9C:40:48:26:91:47:EA:D9:68:18:12
            X509v3 Subject Alternative Name:
                DNS:sample.lab.home, IP Address:127.0.0.1
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage:
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            Authority Information Access:
                OCSP - URI:http://ocsp.lab.home
                CA Issuers - URI:http://ca.lab.home/Home_Lab_CA.crl
            X509v3 CRL Distribution Points:
                Full Name:
                  URI:http://ca.lab.home/Home_Lab_CA.crl
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.2.1
```

### 2.4 mkovcert

Create a certificate with Organisation Validation (OV) extensions.

```
./mkovcert sample.lab.home 127.0.0.1
```

```
Certificate:
    Data:
        Version: 3 (0x2)

        Issuer: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab CA
        Subject: C = AU, ST = Western Australia, L = Perth, O = Home Lab, CN = sample.lab.home

        X509v3 extensions:
            X509v3 Authority Key Identifier:
                E0:88:36:B2:A4:A3:0F:6A:89:D6:30:0E:1E:1A:B3:4A:E1:C6:85:4D
            X509v3 Subject Key Identifier:
                89:07:01:64:32:79:04:FD:DA:DE:E4:CA:4D:A3:CD:3D:4C:55:68:B6
            X509v3 Subject Alternative Name:
                DNS:sample.lab.home, IP Address:127.0.0.1
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage:
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            Authority Information Access:
                OCSP - URI:http://ocsp.lab.home
                CA Issuers - URI:http://ca.lab.home/Home_Lab_CA.crt
            X509v3 CRL Distribution Points:
                Full Name:
                  URI:http://ca.lab.home/Home_Lab_CA.crl
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.2.2
```

### 2.5 mkevcert

Create a certificate with Extended Validation (EV) extensions.

```
./mkevcert sample.lab.home 127.0.0.1
```

```
Certificate:
    Data:
        Version: 3 (0x2)

        Issuer: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab CA
        Subject: businessCategory = Private Organization, jurisdictionC = AU, jurisdictionL = Perth, jurisdictionST = Western Australia, serialNumber = 123 45, street = 123 My Street, postalCode = 6000, C = AU, ST = Western Australia, L = Perth, O = Home Lab, CN = sample.lab.home

        X509v3 extensions:
            X509v3 Authority Key Identifier:
                E0:88:36:B2:A4:A3:0F:6A:89:D6:30:0E:1E:1A:B3:4A:E1:C6:85:4D
            X509v3 Subject Key Identifier:
                69:E8:45:E2:02:BA:0C:E3:EE:E3:DE:92:B7:90:8E:30:86:D3:4D:79
            X509v3 Subject Alternative Name:
                DNS:sample.lab.home, IP Address:127.0.0.1
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage:
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            Authority Information Access:
                OCSP - URI:http://ocsp.lab.home
                CA Issuers - URI:http://ca.lab.home/Home_Lab_CA.crt
            X509v3 CRL Distribution Points:
                Full Name:
                  URI:http://ca.lab.home/Home_Lab_CA.crl
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.1
```

### 2.6 mkself

Create a self signed certificate with extensions include Subject Alternate Name (SAN)

```
./mkself sample.lab.home 127.0.0.1
```

```
Certificate:
    Data:
        Version: 3 (0x2)

        Issuer: C = AU, ST = Western Australia, L = Perth, O = Home, CN = sample.lab.home
        Subject: C = AU, ST = Western Australia, L = Perth, O = Home, CN = sample.lab.home

        X509v3 extensions:
            X509v3 Subject Key Identifier:
                13:C7:DE:54:4C:25:D5:9A:72:A0:2C:C2:E2:0B:91:00:2E:0E:58:17
            X509v3 Authority Key Identifier:
                13:C7:DE:54:4C:25:D5:9A:72:A0:2C:C2:E2:0B:91:00:2E:0E:58:17
            X509v3 Subject Alternative Name:
                DNS:sample.lab.home, IP Address:127.0.0.1
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment, Certificate Sign
            X509v3 Extended Key Usage:
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:TRUE
```

## 3. Certificate Signing Requests

### 3.1 mkcsr

Create a Certificate Signing Request with requested extensions

```
./mkcsr sample.lab.home 127.0.0.1 sample1.lab.home
```

```
Certificate Request:
    Data:
        Version: 1 (0x0)

        Subject: C = AU, ST = Western Australia, L = Perth, O = Home Lab, CN = sample.lab.home

        Attributes:
            Requested Extensions:
                X509v3 Key Usage: critical
                    Key Encipherment, Data Encipherment
                X509v3 Subject Key Identifier:
                    A9:78:20:C6:6F:1E:1C:FF:F3:13:58:EF:10:B1:90:E1:D2:EC:72:61
                X509v3 Subject Alternative Name:
                    DNS:sample.lab.home, IP Address:127.0.0.1, DNS:sample1.lab.home
```

### 3.2 signcsr

Sign a CSR, replacing any extensions to create a certificate with Domain Validated extensions.
> Using the CSR created in 3.1

```
./signcsr sample_lab_home.csr 127.0.0.2 sample2.lab.home
```

```
Certificate:
    Data:
        Version: 3 (0x2)

        Issuer: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab CA
        Subject: OU = Domain Control Validated, OU = homelab, CN = sample.lab.home

        X509v3 extensions:
            X509v3 Authority Key Identifier:
                E0:88:36:B2:A4:A3:0F:6A:89:D6:30:0E:1E:1A:B3:4A:E1:C6:85:4D
            X509v3 Subject Key Identifier:
                A9:78:20:C6:6F:1E:1C:FF:F3:13:58:EF:10:B1:90:E1:D2:EC:72:61
            X509v3 Subject Alternative Name:
                DNS:sample.lab.home, IP Address:127.0.0.2, DNS:sample2.lab.home
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage:
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            Authority Information Access:
                OCSP - URI:http://ocsp.lab.home
                CA Issuers - URI:http://ca.lab.home/Home_Lab_CA.crt
            X509v3 CRL Distribution Points:
                Full Name:
                  URI:http://ca.lab.home/Home_Lab_CA.crl
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.2.1
```

### 3.3 signcsrcp

Sign a CSR, copying the extensions from the CSR and add Domain Validated extensions.
> Using the CSR created in 3.1

```
./signcsrcp sample_lab_home.csr
```

```
Certificate:
    Data:
        Version: 3 (0x2)

        Issuer: C = AU, O = Home Lab, OU = www.lab.home, CN = Home Lab CA
        Subject: OU = Domain Control Validated, OU = homelab, CN = sample.lab.home

        X509v3 extensions:
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.2.1
            X509v3 Key Usage: critical
                Key Encipherment, Data Encipherment
            X509v3 Subject Key Identifier:
                A9:78:20:C6:6F:1E:1C:FF:F3:13:58:EF:10:B1:90:E1:D2:EC:72:61
            X509v3 Subject Alternative Name:
                DNS:sample.lab.home, IP Address:127.0.0.1, DNS:sample1.lab.home
            X509v3 Authority Key Identifier:
                E0:88:36:B2:A4:A3:0F:6A:89:D6:30:0E:1E:1A:B3:4A:E1:C6:85:4D
```
