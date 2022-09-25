# Impostare indirizzo IP statico al raspberry
Prima di iniziare con l'assegnazione di un indirizzo IP privato al Raspberry, controllare che il servizio DHCPCD sia già attivato usando il comando:
```bash
sudo systemctl status dhcpcd
```

In caso il servizio non sia attivo, attivarlo come segue:
```bash
sudo systemctl start dhcpcd
sudo systemctl enable dhcpcd
```

Per prima cosa fare un backup del file di configurazione delle interfacce di rete originale in caso che qualcosa non vada per il verso giusto:
```bash
sudo mv /etc/dhcpcd.conf /etc/dhcpcd.conf.backup
```

Modificare il file di configurazione delle interfacce di rete:
```bash
sudo nano /etc/dhcpcd.conf
```
Aggiungere le seguenti linee alla fine del file (oppure decommentare quelle già esistenti e modificarle opportunamente) per modificare l'interfaccia LAN (rete cablata)
```
interface eth0
static ip_address=192.168.0.4/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1
```
lo stesso vale per la rete wifi ma sostituendo ```eth0``` con ```wlan0```, per esempio:
```
interface wlan0
static ip_address=192.168.0.5/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1
```
> **Note:**
  > 1. Modificare l'indirizzo negli esempi con quello della propria rete locale.
  > 2. Usare indirizzi differenti per la rete cablata e wifi nel caso si voglia utilizzare entrambe le interfacce.

Salvare il file di configurazione con <kbd>CTRL + x</kbd>, <kbd>y</kbd>, <kbd>ENTER</kbd>

Riavviate il sistema
```bash
sudo reboot
```


