# Linux Bootstrap Project

Este projeto utiliza uma role Ansible para automatizar a configuração inicial de máquinas Linux recém-formatadas. Ele foi desenvolvido para suportar distribuições baseadas em Debian e Red Hat, tornando o processo de instalação de softwares e configuração do sistema mais ágil e eficiente.

## Funcionalidades Principais

- Suporte a distribuições baseadas em **Debian** e **Red Hat**.
- Instalação automatizada de ferramentas essenciais como Docker, Rclone, Flatpak, e muito mais.
- Configuração de SSH personalizada, incluindo chaves públicas e privadas.
- Modularidade com tasks organizadas em arquivos YAML, facilitando a manutenção e extensibilidade.

## Tecnologias Utilizadas

- **Ansible**: Para automação da infraestrutura.
- **Linux**: Distribuições Debian e Red Hat como ambiente de destino.
- **Flatpak**: Para instalação de aplicativos adicionais.

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

## Como Utilizar

1. Clone o repositório:

   ```bash
   git clone https://github.com/seuusuario/linux-bootstrap.git
   cd linux-bootstrap
   ```

2. Edite as variáveis no arquivo `vars/main.yml` para personalizar a instalação conforme sua necessidade.

3. Execute o playbook principal com o seguinte comando:

   ```bash
   ansible-playbook -i inventario playbooks/site.yml
   ```

4. Utilize tags para instalar componentes específicos, se necessário:

   ```bash
   ansible-playbook -i inventario playbooks/main.yml --tags "docker,flatpak"
   ```

## Estrutura do Repositório

```plaintext
linux-bootstrap/
├── defaults/          # Variáveis padrão
├── files/             # Arquivos de configuração e chaves
├── tasks/             # Tasks organizadas por distribuição e funcionalidade
├── templates/         # Templates de arquivos de configuração
├── tests/             # Testes automatizados
├── vars/              # Variáveis customizáveis
└── playbooks/         # Playbooks principais
```

## Contribua com Este Projeto

Contribuições são sempre bem-vindas! Se você tiver sugestões, melhorias ou identificar algum problema, sinta-se à vontade para abrir uma issue ou enviar um pull request.

---

Feito com ❤️ e dedicação por **Marco Tulio**.