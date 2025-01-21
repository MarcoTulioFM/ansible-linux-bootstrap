# Linux Bootstrap Role

Esta role Ansible foi criada para automatizar a configuração inicial e instalação de softwares em máquinas Linux recém-formatadas. Ela é compatível com distribuições baseadas em Debian (como Ubuntu, Zorin OS e Pop!_OS) e Red Hat (como Fedora e Rocky Linux).

## Funcionalidades

- **Suporte a múltiplas distribuições:**
  - Debian-based (apt)
  - Red Hat-based (dnf)
- **Instalação e configuração de softwares:**
  - Docker
  - Rclone
  - Flatpak (com pacotes adicionais)
  - Visual Studio Code
  - Terraform
  - Tailscale
  - Zen Browser
- **Configuração de SSH:**
  - Chaves públicas e privadas
  - Pastas de configuração personalizadas
- **Gerenciamento modular:**
  - Tasks organizadas por arquivos YAML para facilitar a manutenção

## Estrutura do Projeto

```plaintext
linux-bootstrap/
├── defaults/
│   └── main.yml          # Variáveis padrão
├── files/
│   ├── rclone/
│   │   └── rclone.conf   # Configuração do Rclone
│   ├── ssh/
│       ├── geral         # Chave SSH privada
│       └── geral.pub     # Chave SSH pública
├── tasks/
│   ├── debian/
│   │   ├── debian.yaml   # Tasks específicas para Debian
│   │   ├── terraform.yaml
│   │   └── vscode.yaml
│   ├── redhat/
│       ├── redhat.yaml   # Tasks específicas para Red Hat
│       ├── terraform.yaml
│       ├── docker.yaml
│       ├── flatpak.yaml
│       ├── rclone.yaml
│       ├── ssh.yaml
│       ├── tailscale.yaml
│       └── zen.yaml
├── templates/
│   └── ...               # Arquivos de templates (caso aplicável)
├── tests/
│   └── ...               # Testes para a role
├── vars/
│   └── main.yml          # Variáveis customizáveis
└── playbooks/
    └── ...               # Playbooks de exemplo
```

## Pré-requisitos

- Ansible 2.9+
- Distribuição Linux compatível (Debian-based ou Red Hat-based)
- Usuário com permissões de `sudo`

## Variáveis Principais

As variáveis podem ser ajustadas no arquivo `vars/main.yml`. Aqui está uma descrição delas:

```yaml
# Lista de pacotes para instalação em distribuições baseadas em Debian
# Exemplo: ["htop", "vim", "git"]
debian_package: []

# Lista de pacotes para instalação em distribuições baseadas em Red Hat
# Exemplo: ["vim", "git", "curl"]
redhat_package: []

# Caminho para scripts temporários
# Exemplo: "/tmp"
past_script: ""

# Usuário para configuração
# Exemplo: "seu_usuario"
user: ""

# Lista de pacotes Flatpak para instalar
# Exemplo: ["com.bitwarden.desktop", "com.getpostman.Postman"]
flatpak_packages: []

# Caminhos personalizados para ferramentas
# Exemplo: ".var/app/io.github.zen_browser.zen/.zen"
zen_path: ""
vscode_path: ""
rclone_path: ""
distro_release: ""
arch: ""
```

## Inventário de Exemplo

O arquivo de inventário pode ser personalizado para atender ao seu ambiente. Aqui está um exemplo:

```yaml
all:
  children:
    dnf:
      hosts:
        redhat_host:
          ansible_host: '<IP_DO_HOST_RED_HAT>' # Substitua pelo IP do seu host Red Hat
    apt:
      hosts:
        debian_host:
          ansible_host: '<IP_DO_HOST_DEBIAN>' # Substitua pelo IP do seu host Debian
    linux:
      children:
        dnf:
        apt:
```

## Uso

1. Clone o repositório:

   ```bash
   git clone https://github.com/seuusuario/linux-bootstrap.git
   cd linux-bootstrap
   ```

2. Altere as variáveis conforme necessário no arquivo `vars/main.yml`.

3. Execute a role:

   ```bash
   ansible-playbook -i inventario playbooks/site.yml
   ```

## Tags Disponíveis

Use tags para executar tasks específicas. Exemplo:

```bash
ansible-playbook -i inventario playbooks/site.yml --tags "docker,ssh"
```

Tags principais:
- `docker`
- `rclone`
- `flatpak`
- `terraform`
- `tailscale`
- `browser`

## Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests.

---

Feito com 💻 e ⚙️ por Marco Tulio
