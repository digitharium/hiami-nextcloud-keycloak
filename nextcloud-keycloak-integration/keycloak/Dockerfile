FROM quay.io/keycloak/keycloak:latest

COPY wait-for-it /opt/
COPY create_realm_and_client.sh /opt/

ENTRYPOINT ["/opt/keycloak/bin/kc.sh", "start-dev"]