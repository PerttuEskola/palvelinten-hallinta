# h4 Pizza Fantasia

## x) Karvinen 2023
- DSL:t ovat suuria ja monimutkaisia, esim. Saltin dokumentaatio ylittää väitöskirjan pituuden.
- Ylläpitäjät käyttävät oikeasti vain pientä osaa sadoista funktioista.
- Useimmat korkeamman tason toiminnot voidaan rakentaa kahden perusfunktion (file ja exec) varaan.


## a) Räpylä
### Asennetaan Redis
````
sudo apt update
````
````
sudo apt install redis-server
````
### Käynnistetään Redis
````
sudo systemctl start redis-server
````
````
sudo systemctl enable redis-server
````
### Testataat että redis toimii.
````
redis-cli ping
````
### Kun redis vastaa PONG se on käynnissä, käytössä ja toimiva.
<img width="634" height="63" alt="image" src="https://github.com/user-attachments/assets/198f3bd7-eaab-441b-94ea-d1b6ca563a4d" />

## b) Automaatti
### Luodaan kansio rakenne.
````
└── roles/
    └── redis/
        ├── tasks/
        │   └── main.yml
        ├── handlers/
        │   └── main.yml
        └── files/
            └── redis.conf
````
### tasks/main.yml
#### Asennetaan itse demoni ja luodaan mahdollisuus lisätä konfigurointi tiedosto. Muistutetaan uudelleen käynnistys.
<img width="491" height="463" alt="image" src="https://github.com/user-attachments/assets/7bcd113e-0ff9-4751-b77a-ac05db5660c5" />

### handlers/main.yml
#### Uudelleen käynnistys.
<img width="329" height="137" alt="image" src="https://github.com/user-attachments/assets/494617fc-9689-4d3a-b861-1389433ead2b" />

### Lisätään redis rooli site.yml
<img width="273" height="143" alt="image" src="https://github.com/user-attachments/assets/72d18b8d-28a2-442a-80a0-13a8caf64b17" />

### Ajetaan ansible playbook
````
ansible-playbook site.yml --ask-become-pass
````
### Ansible suoritti ajon, Redis toimii.
<img width="1089" height="853" alt="image" src="https://github.com/user-attachments/assets/9e9a3e1d-7993-4cfe-a7d6-b719ea7b05fc" />

## c) Asetus
### Vaihdetaan oletus portti 6379 porttiin 7777 ja testataan portit ennen vaihtoa.
<img width="930" height="119" alt="image" src="https://github.com/user-attachments/assets/9308de0b-9545-43b4-9f40-78448e882737" />


### Muutetaan tasks/main.yml tiedostoa.
#### Muutetaan 'port' alkava rivi port 7777, redis.conf tiedostossa.
<img width="907" height="360" alt="image" src="https://github.com/user-attachments/assets/d0c5dd82-f440-4f60-b3df-9d9c4ddaa038" />

### Ajetaan ansible playbook
<img width="1054" height="765" alt="image" src="https://github.com/user-attachments/assets/4d1552b9-4ac1-4f01-9cac-a8f16e791db1" />

### Testataan portteja.
<img width="866" height="124" alt="image" src="https://github.com/user-attachments/assets/65fe85f7-249d-4595-96bf-b78f0e58cb07" />

## d) Paikka remonttiin
### Poistetaan demoni.
````
sudo apt purge --auto-remove redis-server
````
<img width="1076" height="619" alt="image" src="https://github.com/user-attachments/assets/a81cd360-d348-4d57-93be-9b3c0a84511d" />

### Testataan aikaisemmin ajettua komentoa
<img width="785" height="65" alt="image" src="https://github.com/user-attachments/assets/f5de4199-c31e-4738-a3a9-f3356f581f6a" />

### Ajetaan playbook
<img width="1045" height="765" alt="image" src="https://github.com/user-attachments/assets/15d0260e-a384-44ea-8221-56aec961013d" />


### Testataan aikaisemmin ajettua komentoa
<img width="783" height="64" alt="image" src="https://github.com/user-attachments/assets/1f873371-c507-4020-947e-415c625edf10" />

## e) Idempotentti
### Ajetaan ansible playbook vielä kerran ja voidaan todeta että tila on idempotentti.
<img width="1043" height="646" alt="image" src="https://github.com/user-attachments/assets/b45466ed-733a-42dd-a876-ee102479a79e" />

## Lähteet
- Redis.io: https://redis.io/docs/latest/operate/oss_and_stack/install/archive/install-redis/
- Karvinen 2023: https://westminsterresearch.westminster.ac.uk/item/w7vvz/configuration-management-of-distributed-systems-over-unreliable-and-hostile-networks
- Gemini: https://gemini.google.com/
- ChatGPT: https://chatgpt.com/
