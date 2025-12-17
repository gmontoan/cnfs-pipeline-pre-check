# Ansible Project Template

This repository is a template for an `Ansible Project` that includes the typical Ansible structure.

- [.config](.config) folder contains lint rules and other configuration
- [.github](.github) folder contains GitHub workflow action configuration
- [collections](./collections/) folder contains definitions of Ansible Collections
- [roles](./roles/) folder contains definitions of Ansible Roles
- [hosts](./hosts/) folder contains Ansible inventory and configuration management with group variables
- [plugins](./plugins/) folder contains custom Ansible plugins for inventory, filter, action, callback, and so on
- [playbooks](./playbooks/) folder contains Ansible Playbooks to perform actions
- Code Quality Tests are performed using various linting tools
  - Ansible Lint
  - Ruff for Python linting

Recommended `Visual Studio Code` extensions that help to manage this repository:

- Ansible
- Ruff
- Even Better TOML

## Examples

Use this repository to run some of the following useful commands:

```shell
# Ansible Dev Tools https://ansible.readthedocs.io/projects/dev-tools/
pip install ansible-dev-tools
adt --version

# Using ansible-playbook command
ansible-playbook -i hosts/dev/inventory playbooks/aap_content.yml
# Using ansible-navigator command - [ansible-navigator demo](https://www.youtube.com/watch?v=J9PBKi8ydi4)
ansible-navigator run -i hosts/dev/inventory playbooks/aap_content.yml

# Linting current project using ansible-lint
ansible-lint
# Linting current project using ansible-navigator
ansible-navigator lint $CWD
# Fix linting errors
ansible-lint --fix
# Generate ignore file
ansible-lint --generate-ignore

# Linting Python files (modules, plugins, etc)
ruff check
# Fixing Python linting errors
ruff check --fix
# Show statistics to show counts for every rule
ruff check --statistics
# List python files detected
ruff check --show-files
# Format Python files correctly
ruff format <python file>

# Check configuration inside image using ansible-navigator
ansible-navigator config dump
# Check collections using interactive mode
ansible-navigator collections --mode=interactive
```

Com base no guia Red Hat Best Practices for Kubernetes foi desenvolvido um playbook de auditoria de segurança.

Este guia enfatiza fortemente a segurança dos workloads (Pods), evitando privilégios excessivos, montagens de host e garantindo a saúde da aplicação (Probes) e governança de recursos.

O que este Playbook Audita?
Baseado nos capítulos 2.12 (Pod Security), 3.5 (Workload Security), 3.6 (Capabilities) e 3.12 (Cloud-native design):

Privileged Containers: Pods rodando com privileged: true (Violação Crítica).

HostPath Volumes: Pods montando diretórios do nó host (Violação de Isolamento).

Capabilities Perigosas: Uso de SYS_ADMIN, NET_ADMIN, etc.

Imagens inseguras: Uso da tag :latest (Violação de Imutabilidade).

Falta de Probes: Pods sem Liveness/Readiness probes configurados.

Falta de Limites: Pods sem Requests/Limits de CPU e Memória (Risco de DoS).

Network Policies: Namespaces sem políticas de rede (Isolamento de Rede).
