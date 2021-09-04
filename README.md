# Docker-LDAP-Account-Manager
docker-compose.yml

```
version: '3.5'
services:
  ldap-account-manager:
    image: ldapaccountmanager/lam:latest
    network_mode: bridge
    restart: unless-stopped
    container_name: lam 
    build:
      context: .
    ports:
      - "8080:80"
    volumes:
      - ldap-account-manager:/var/lib/ldap-account-manager/config
   
    environment:
      - LAM_PASSWORD=lam
      - LAM_LANG=en_US
      - LDAP_SERVER=ldap://172.17.0.1:389
      - LDAP_DOMAIN=my-domain.com
      - LDAP_BASE_DN=dc=my-domain,dc=com
      - ADMIN_USER=cn=admin,my-domain
      - DEBUG=true
volumes:
  ldap-account-manager:
    external: true

networks: 
  default: 
    external: 
      name: bridge
