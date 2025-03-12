
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

### `install_nginx.yml`

O playbook `install_nginx.yml` é responsável por instalar e configurar o Nginx nos servidores definidos no arquivo de inventário. Ele executa três tarefas principais:

1. **Atualizar pacotes APT**:
    - Atualiza o cache dos pacotes APT no servidor alvo.
  
2. **Instalar Nginx**:
    - Instala o pacote Nginx no servidor.

3. **Iniciar e habilitar Nginx**:
    - Inicia o serviço Nginx e o configura para iniciar automaticamente na inicialização do sistema.

## Como Usar

### 1. Modificar os Arquivos

Edite os arquivos com as informações corretas do seu servidor, substituindo os placeholders:

- **`<server_name>`**: Nome do servidor.
- **`<server_ip>`**: IP do servidor.
- **`<username>`**: Usuário para autenticação.
- **`<path_to_private_key>`**: Caminho para a chave privada usada para autenticação SSH.

### 2. Executar o Playbook

Execute o playbook com o comando Ansible:

```bash
ansible-playbook -i hosts.ini install_nginx.yml
```

Isso fará com que o Ansible conecte-se aos servidores definidos no `hosts.ini` e execute as tarefas para instalar e configurar o Nginx.

