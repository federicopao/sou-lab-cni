Il Vagrantfile crea 2 nodi e richiama il playbook nel quale sono definiti 2 ruoli
ogni ruolo esegue le task a lui assegnate su uno dei due nodi:
```
- hosts: node1
  become: yes
  roles:
    - docker_haproxy
       

- hosts: node2
  become: yes
  roles:
    - docker_prometheus_grafana
```

In un nodo è installato HaProxy in un container,
nell'altro nodo sono presenti Grafana e Prometheus, ognuno nel suo container, poi abbiamo il node exporter installato e il container con cadvisor.

Prometheus riceve le metriche da un node exporter in modo tale da monitore lo stato della macchina node2.
per attivare il node exporter eseguire i seguenti comandi:

```
vagrant ssh node2

cd node_exporter-0.18.1.linux-arm64
./node_exporter

sudo docker restart prometheus
```

In seguito nel browser verificare che prometheus sia connesso al node exporter e al cadvisor all'indirizzo:

```
http://192.168.56.22:9090/targets
```

L'Haproxy è configurato in modo tale da operare come reverse proxy per Grafana.

Le configurazioni necessarie sono definite nella cartella templates del rispettivo ruolo,
l'Haproxy è configurato in modo tale che inserendo il suo IP con la porta 8080 si connette a grafana che a sua volta potrà essere connesso a prometheus.
Prometheus ha all'attivo una configurazione base che ha lo scopo solo di vedere se l'applicativo fosse in grado di connettersi a grafana.

