# Demoni
## x) 
### Karvinen 2026
- Esittelee, miten Apache-verkkopalvelin asennetaan automaattisesti Ansiblella.
- Palvelimen konfigurointi niin, että verkkosivuja voi muokata tavallisena käyttäjänä ilman sudo-oikeuksia.

### Ansible Community Documentation
- Handlerit ovat tehtäviä, jotka suoritetaan vain silloin, kun jokin toinen tehtävä on tehnyt muutoksen järjestelmässä.
- Tehtävät kutsuvat handlereita notify-sanalla, ja kutsu lähetetään vain, jos tehtävän tila on "changed".
- Vaikka useampi tehtävä kutsuisi samaa handleria, handeri suoritetaan vain kerran.

### ansible.builtin.service
- Moduulia käytetään palveluiden hallintaan etäkoneilla.
- Se tukee useita eri init-järjestelmiä.
- name: Palvelun nimi, jota halutaan hallita.
- state: Määrittää palvelun tilan.
- enabled: Määrittää, käynnistetäänkö palvelu automaattisesti järjestelmän käynnistyessä.


## a) Apache2
### Asennetaan apache2.
````
sudo apt update
sudo apt install apache2
````
### Luodaan kotisivukansio ja sen sisälle index.html.
````
mkdir publicsite
nano publicsite/index.html
````
### index.html sisälle tekstiä.
````html
<h1>Apache testi</h1>
````
### Lisätään oikeudet tiedostoon.
<img width="1056" height="100" alt="image" src="https://github.com/user-attachments/assets/46dff36c-786c-4029-aafa-c6b3800cab90" />

### Muutetaan apachen konfiguraatiota.
````bash
sudo nano /etc/apache2/sites-available/000-default.conf
````
<img width="961" height="453" alt="image" src="https://github.com/user-attachments/assets/65215e37-7151-497d-9770-8996427fa5cd" />

### Käynnistetään apache uudestaan.
````bash
sudo systemctl restart apache2
````
### Verkkosivu näyttää nyt tältä.
<img width="572" height="192" alt="image" src="https://github.com/user-attachments/assets/acf490a7-6940-4cfe-a226-d2a6366572cf" />

### Apachen sammutus.
````bash
sudo systemctl stop apache2
````
### Jonka jälkeen verkkosivu sammuu.
<img width="609" height="408" alt="image" src="https://github.com/user-attachments/assets/5c0bc921-a871-4b07-aaf9-c88acd4b2aae" />


## b) Nginx

### Asennetaan nginx.
````bash
sudo apt update
sudo apt install nginx
````
### Muokataan nginxin konfiguraatiota.
````bash
sudo nano /etc/nginx/sites-available/default
````
<img width="472" height="85" alt="image" src="https://github.com/user-attachments/assets/6254f11f-d2fd-4b45-bcf6-271917ebc527" />

### Käynnistetään nginx uudelleen.
````bash
sudo systemctl restart nginx
````
### Verkkosivu taas päällä
<img width="585" height="322" alt="image" src="https://github.com/user-attachments/assets/a8c7da0a-2d2d-412d-90e0-5464d41a308b" />

## c) Automatisointi

### Tehdään kansiorakenne ansibleen.
````
.
└── roles/
    └── nginx/
        ├── files/
        │   └── default
        ├── handlers/
        │   └── main.yml
        └── tasks/
            └── main.yml
````
### files/default configurointi tiedosto
<img width="851" height="512" alt="image" src="https://github.com/user-attachments/assets/949c04fa-f97c-4564-9120-4d06605f3d24" />

### handlers/main.yml
<img width="415" height="184" alt="image" src="https://github.com/user-attachments/assets/5bd24b2a-fad6-454b-b0b2-6f836b2100a5" />

### tasks/main.yml
<img width="717" height="502" alt="image" src="https://github.com/user-attachments/assets/49ff7abb-b7c5-473d-9d68-f6a017975266" />

### Lisätään nginx site.yml
<img width="274" height="166" alt="image" src="https://github.com/user-attachments/assets/47a62280-eead-4cdc-9dec-a2e99162aa5b" />

### Suoritetaan site.yml
````bash
ansible-playbook site.yml --ask-become-pass
````
<img width="1136" height="460" alt="image" src="https://github.com/user-attachments/assets/b882765b-5dc1-4c18-b749-d9f3ce396096" />

## Lähteet
- Karvinen 2026: Apache installed with Ansible https://terokarvinen.com/apache-ansible/ 
- Ansible Community Documentation: https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html#notifying-handlers
