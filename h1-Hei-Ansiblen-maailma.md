

x)
  - SSH on turvallinen tapa kirjautua palvelimelle. 
  - Julkinen avain mahdollistaa kirjautumisen ilman salasanaa.
  - SSH avaimet helpttavat, sillä salasanaa ei tarvitse laittaa joka kerta.
  - Teksissä kerrotaan SSH:n asennus ja avainten automatisointi.

  - Ansible on konfikuraation työkalu, käytetään konfiguroimaan ja ylläpitämään monia koneita saman aikaisesti.
  - Toimii ssh:n yli.
  - Tektissä kerrotaan Ansible asennus ja tiedoston luominen. 


a)
  sudo apt-get update
  sudo apt-get -y install ssh
  sudo systemctl enable --now ssh
  ssh perttu@localhost

b)
  ssh-keygen
  ssh-copy-id perttu@localhost

c)
  sudo apt-get update
  sudo apt-get install ansible micro bash-completion tree
  mkdir ansible/
  cd ansible/
  micro hosts.ini --- sisään perttu@localhost
  ansible all -a 'uptime' -i hosts.ini
  mkdir -p roles/hello/tasks
  micro roles/hello/tasks/main.yml
  
  - copy:
    dest: /tmp/hello-ansible
    content: "Hei maailma\n"
  
  micro site.yml
  
  - hosts: all
      roles:
        - hello
          
  ansible-playbook -i hosts.ini site.yml
  
  ssh localhost 'cat /tmp/hei-ansible'

  tulostus: Hei maailma
  
  
