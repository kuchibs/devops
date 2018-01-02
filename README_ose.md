# OSE on 1 vm
# Install docker from RedHat/CentOS repos
yum install docker
# Include the local registry
echo "INSECURE_REGISTRY='--insecure-registry 172.30.0.0/16'" >> /etc/sysconfig/docker
systemctl enable docker
systemctl start docker

# Install OpenShift client
cd /root
wget https://github.com/openshift/origin/releases/download/v1.5.0/openshift-origin-client-tools-v1.5.0-031cbe4-linux-64bit.tar.gz
tar -xvzf openshift-origin-client-tools-v1.5.0-031cbe4-linux-64bit.tar.gz
mkdir -p /usr/local/bin
mv openshift-origin-client-tools-v1.5.0-031cbe4-linux-64bit/* /usr/local/bin/

# Start the cluster
oc cluster up

 firewall-cmd --list-all 
 
 firewall-cmd --permanent --add-port=8443/tcp
 
 firewall-cmd --permanent --add-port=53/udp
 
 firewall-cmd --permanent --add-service=https
 firewall-cmd --permanent --add-service=http
 firewall-cmd --reload
 firewall-cmd --list-all
