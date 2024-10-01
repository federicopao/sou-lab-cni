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
nell'altro nodo sono presenti Grafana e Prometheus, ognuno nel suo container.

L'Haproxy è configurato in modo tale da operare come reverse proxy per Grafana.


