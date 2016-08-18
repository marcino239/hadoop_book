# Java
## SSL
This is required for self-signed or internally signed certificates. Another option is to change `cacerts` for the Java installation.

### Add Certificate to a Truststore
```bash
openssl s_client -showcerts -connect ${SSLHOST}:${SSLPORT} </dev/null 2>/dev/null > ${SSLHOST}.crt
keytool -import -keystore ${TRUSTSTORE_PATH}.jks -file ${SSLHOST}.crt -storepass ${TRUSTSTORE_PASSWORD} -alias $SSLHOST -noprompt
rm ${SSLHOST}.crt
```

### Use Truststore
```bash
java \
  ... \
  -Djavax.net.ssl.trustStore=${TRUSTSTORE_PATH}.jks \
  -Djavax.net.ssl.trustStorePassword=${TRUSTSTORE_PASSWORD} \
  ... \
  MainClass \
  Args...
```

## Kerberos
```bash
java \
  ... \
  -Djava.security.auth.login.config=PATH_TO_JAAS.conf  \
  ... \
  MainClass \
  Args...
```

### JAAS
* https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html
* https://steveloughran.gitbooks.io/kerberos_and_hadoop/content/sections/jaas.html

#### Ticket Cache
```
Client {
  com.sun.security.auth.module.Krb5LoginModule required
  useTicketCache=true;
};
```

#### Keytab
```
Client {
  com.sun.security.auth.module.Krb5LoginModule required
  useTicketCache=false
  useKeyTab=true
  principal="principal@EXAMPLE.COM"
  keyTab="PATH_TO_KEYTAB.keytab"
  renewTicket=true
  storeKey=true;
};
```