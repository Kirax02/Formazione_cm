# Obbiettivo
## Creare un playbook che configuri un docker registry (anche senza autenticazione)

Questo playbook Ansible configura ed avvia un Docker Registry locale sulla macchina host senza autenticazione. Il registry memorizzerà i dati persistenti in una directory specificata.
## Spiegazione task playbook

### Task:
```yaml
    - name: Create directory for registry data
      file:
        path: "/Users/lorenzomoro/registry"
        state: directory
```
Con la seguente task viene creata una directory locale dove memorizzare i file.

### Task:
```yaml
    - name: Run Registry container
      community.docker.docker_container:
        name: registry
        image: registry:2
        state: started
        restart_policy: always
        ports:
          - "5000:5000"
        volumes:
          - "/Users/lorenzomoro/registry:/var/lib/registry"
```
Con la seguente task viene creato il container registry, montando il volume per la memorizzazione dei file.
