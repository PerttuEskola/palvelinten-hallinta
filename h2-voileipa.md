# Voileipä
## x)
### Sudo without password
- Luodaan ryhmä, jolle annetaan sudo-oikeudet ilman salasanaa.
- Listätään sääntö sudoers-tiedostoon.
- Sen jälkeen ryhmän käyttäjät voivat ajaa komentoja root-oikeuksilla ilman salasanaa.
- Tämä nopeuttaa käyttöä mutta heikentää tietoturvaa

### Sandwich
- Sudolla saa tehtyä kaikenlaista

### Passwordless Sudo with Ansible
- Tässä tehdään Ansible-rooli, joka automatisoi salasanattoman käyttäjän luomisen.
- Luo käyttäjän antero, lisää hänet sudoless ryhmään, antaa SSH-avainkirjautumisen ja tekee sudoers-säännön /etc/sudoers.d/-hakemistoon.
- Ryhmä voi käyttää sudoa ilman salasanaa.



## a)
Luodaan käyttäjä bossi sudoless ryhmän

<img width="817" height="471" alt="image" src="https://github.com/user-attachments/assets/d8f4140c-4a84-49e8-814a-e90d7a8d2596" />


luodaan sudoless oikeudet
```
sudo visudo /etc/sudoers.d/sudoless
```
ja sisään 
```
%sudoless ALL = (ALL) NOPASSWD: ALL
```
## b)
luodaan tiedosto ja kansiot roles/jari/tasks/main.yml

<img width="1147" height="571" alt="image4" src="https://github.com/user-attachments/assets/e262ad02-1cce-4a46-9fb5-b6edb683c2c9" />

lisätään become: true ja rooli 

<img width="231" height="181" alt="image3" src="https://github.com/user-attachments/assets/f9d8b6f9-f800-4f4d-9010-af284bde4491" />

Suoritetaan luotu tiedosto.

<img width="1150" height="1075" alt="image7" src="https://github.com/user-attachments/assets/286c9165-9752-43f4-918f-100f10d07936" />

## c)
Tehdään paketit.yml jonne luodaan pakettien asennus

<img width="755" height="414" alt="image5" src="https://github.com/user-attachments/assets/035980d8-30d2-416a-b128-24430c325084" />

Testataan paketit.yml

<img width="1153" height="692" alt="image6" src="https://github.com/user-attachments/assets/a54fa6bf-3407-49aa-baf5-f78e84c2db9d" />

## d)
Luodaan usemmaan rivin mittainen tiedosto ja selitetään oikeudet.

<img width="908" height="566" alt="image8" src="https://github.com/user-attachments/assets/7c3adb9d-f8a2-4e0c-bafc-98bcaa66a8f2" />

Testataan tiedosto

<img width="1141" height="661" alt="image9" src="https://github.com/user-attachments/assets/aeb309e7-e277-43f2-8edf-1d308230b904" />

## e) 
Tehdään ansiblella uusi kansio kohteena hosts.inissä all

<img width="1143" height="727" alt="image10" src="https://github.com/user-attachments/assets/9114da8d-1e4d-4cdd-ab15-55bdf5b10376" />

