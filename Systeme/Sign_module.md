# Signer un module sous linux

## Etape 1 :

- On génère une clé privée et une clé publique

### On crée un fichier openssl.cnf

```
HOME                    = .
RANDFILE                = $ENV::HOME/.rnd 
[ req ]
distinguished_name      = req_distinguished_name
x509_extensions         = v3
string_mask             = utf8only
prompt                  = no

[ req_distinguished_name ]
countryName             = A_modifier
stateOrProvinceName     = A_modifier
localityName            = A_modifier
organizationName        = A_modifier
organizationalUnitName  = A_modifier
commonName              = A_modifier
emailAddress            = A_modifier

[ v3 ]
subjectKeyIdentifier    = hash
authorityKeyIdentifier  = keyid:always,issuer
basicConstraints        = critical,CA:FALSE
extendedKeyUsage        = codeSigning,1.3.6.1.4.1.2312.16.1.2
nsComment               = "OpenSSL Generated Certificate"
```

### On génère la clé privée et la clé publique

```
openssl req -config ./openssl.cnf \
        -new -x509 -newkey rsa:2048 \
        -nodes -days 36500 -outform DER \
        -keyout "MOK.priv" \
        -out "MOK.der"
```

## Etape 2 :

- On importe la clé publique dans le keystore de la machine

```
sudo mokutil --import MOK.der
```

## Etape 3 :

- Redémarrez le système et le programme d'installation MOK apparaîtra.
- Suivez les instructions pour ajouter la clé de signature à la liste des clés de signature approuvées pour Secure Boot.

## Etape 4 :

- On montre les infos du modules, on vérifie si il est bien installé et on récupère le chemin du module

```
modinfo evdi
```

- On signe le module

```
openssl x509 -in MOK.der -inform DER -outform PEM -out /home/MOK.pem
sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 MOK.priv /home/MOK.pem /Le/chemin/du/module
```

## Etape 5 :

- On redémarre la machine

## Etape 6 :

- On vérifie que le module est bien signé

```
modinfo evdi
```
