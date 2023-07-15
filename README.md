# Repository belajar jenkins

Code by Programmer Zaman Now

### Vagrantfile untuk create VM Jenkins
```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "4098"
    vb.cpus = 4
  end

  config.vm.define "jenkins-vm" do |jenkins|
    jenkins.vm.network :private_network, ip: "192.168.1.12"
  end
end
```

### Connect ke VM Jenkins dengan Port Forwarding ke Port 1212 
```bash
ssh -D 1212 vagrant@192.168.1.12 -p 22 -i /home/febrian/Vagrant/belajar-jenkins/.vagrant/machines/jenkins-vm/virtualbox/private_key 
```
### Agar VM bisa diakses menggunakan domain
```java
127.0.0.1	localhost
192.168.1.12	jenkins.vm

# The following lines are desirable for IPv6 capable hosts
::1	ip6-localhost	ip6-loopback
fe00::0	ip6-localnet
ff00::0	ip6-mcastprefix
ff02::1	ip6-allnodes
ff02::2	ip6-allrouters
ff02::3	ip6-allhosts
127.0.1.1	ubuntu-jammy	ubuntu-jammy
```
### Setting SSL Certificate agar Jenkins bisa diakses dengan HTTPS
```bash
openssl req -newkey rsa:2048 -nodes -keyout jenkins-vm-key.pem -x509 -days 365 -out jenkins-vm-cert.pem
openssl pkcs12 -inkey jenkins-vm-key.pem -in jenkins-vm-cert.pem -export -out jenkins-vm-cert.p12
keytool -importkeystore -srckeystore jenkins-vm-cert.p12 -srcstoretype pkcs12 -destkeystore jenkins-vm.jks -deststoretype JKS
```
### Running Jenkins dengan HTTPS 
```bash
java -jar jenkins.war --httpsPort=443 --httpPort=-1 --httpsKeyStore=jenkins-vm.jks --httpsKeyStorePassword="rahasia" &
```
![image](https://github.com/febri4n/jenkins-playground/assets/18482250/0c8ac246-2a1a-4852-b218-da1c50477db1)

![image](https://github.com/febri4n/jenkins-playground/assets/18482250/0f98931a-12bb-40cb-b05a-82518f2f4bb6)
