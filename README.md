Il Vagrantfile crea 2 nodi e richiama il playbook. 

Su uno gira HaProxy in un container, nell'altro abbiamo Grafana e Prometheus in due container.

L'Haproxy è configurato in modo tale da operare come reverse proxy per Grafana.
