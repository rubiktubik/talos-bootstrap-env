FROM debian:bookworm-slim

RUN apt-get update
RUN apt install -y dialog nmap curl apt-transport-https ca-certificates gnupg

# Prepare everything for kubectl installation
RUN mkdir -p -m 755 /etc/apt/keyrings
RUN curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
RUN chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg
RUN echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | tee /etc/apt/sources.list.d/kubernetes.list
RUN chmod 644 /etc/apt/sources.list.d/kubernetes.list 

RUN apt-get update
RUN apt install -y kubectl

RUN curl -sL https://talos.dev/install | sh

RUN curl -LO https://github.com/aenix-io/talos-bootstrap/raw/master/talos-bootstrap
RUN chmod +x talos-bootstrap && mv talos-bootstrap /usr/local/bin