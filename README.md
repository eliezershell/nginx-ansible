
# Playbook Ansible para Instalar e Configurar o Nginx

Este repositório contém um exemplo de playbook Ansible para instalar e configurar o Nginx em servidores remotos. Ele usa um arquivo de inventário (`hosts.ini`) e um playbook (`install_nginx.yml`) para realizar as tarefas necessárias.

## Estrutura do Repositório

```
.
├── hosts.ini
└── install_nginx.yml
```

### `hosts.ini`

O arquivo `hosts.ini` contém a configuração do inventário, onde você define os servidores nos quais o Ansible deve atuar. O formato é o seguinte:

```ini
[servers]
<server_name> ansible_host=<server_ip> ansible_user=<username> ansible_private_key_file=<path_to_private_key>
```

- **`<server_name>`**: Nome do servidor (pode ser qualquer nome representativo, como `webserver1`).
- **`<server_ip>`**: Endereço IP do servidor.
- **`<username>`**: Usuário para autenticação SSH (por exemplo, `ubuntu`, `ec2-user`, etc.).
- **`<path_to_private_key>`**: Caminho para o arquivo da chave privada usada para autenticação.

### `install_nginx.yml`

O playbook `install_nginx.yml` é responsável por instalar e configurar o Nginx nos servidores definidos no arquivo de inventário. Ele executa três tarefas principais:

1. **Atualizar pacotes APT**:
    - Atualiza o cache dos pacotes APT no servidor alvo.
  
2. **Instalar Nginx**:
    - Instala o pacote Nginx no servidor.

3. **Iniciar e habilitar Nginx**:
    - Inicia o serviço Nginx e o configura para iniciar automaticamente na inicialização do sistema.

O arquivo `install_nginx.yml` é o seguinte:

```yaml
- name: Instalar e Configurar Nginx
  hosts: <server_name>
  become: true
  tasks:
    - name: Atualizar pacotes APT
      apt:
        update_cache: yes

    - name: Instalar Nginx
      apt:
        name: nginx
        state: present

    - name: Iniciar e habilitar Nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

## Como Usar

### 1. Modificar o Arquivo de Inventário

Edite o arquivo `hosts.ini` com as informações corretas do seu servidor, substituindo os placeholders:

- **`<server_name>`**: Nome do servidor.
- **`<server_ip>`**: IP do servidor.
- **`<username>`**: Usuário para autenticação.
- **`<path_to_private_key>`**: Caminho para a chave privada usada para autenticação SSH.

Exemplo:

```ini
[servers]
myserver1 ansible_host=192.168.1.100 ansible_user=ubuntu ansible_private_key_file=~/.ssh/mykey.pem
```

### 2. Executar o Playbook

Execute o playbook com o comando Ansible:

```bash
ansible-playbook -i hosts.ini install_nginx.yml
```

Isso fará com que o Ansible conecte-se aos servidores definidos no `hosts.ini` e execute as tarefas para instalar e configurar o Nginx.

## Contribuições

Sinta-se à vontade para abrir problemas (issues) ou enviar pull requests para melhorar este repositório.

## Licença

Este repositório está licenciado sob a [MIT License](LICENSE).
