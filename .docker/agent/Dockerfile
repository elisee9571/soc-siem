# Utiliser une image Ubuntu de base avec architecture 64 bits
FROM ubuntu:24.04

# Installer les dépendances
RUN apt-get update && apt-get install -y curl gnupg apt-transport-https sudo

# Ajouter la clé GPG de Wazuh et le dépôt
RUN curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | apt-key add - && \
    echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | tee /etc/apt/sources.list.d/wazuh.list

# Mettre à jour les paquets et installer l'agent Wazuh
RUN apt-get update && apt-get install -y wazuh-agent

# Configurer l'agent Wazuh pour se connecter au serveur Wazuh (à adapter)
COPY ossec.conf /var/ossec/etc/ossec.conf

# Exposer le port pour la communication avec le serveur Wazuh si nécessaire
EXPOSE 1514/udp

# Lancer l'agent Wazuh en premier plan pour éviter que le conteneur ne s'arrête
CMD ["/var/ossec/bin/wazuh-control", "start", "agent"]
