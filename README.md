# Ponderada - Design de Arquitetura MVC


# Arquitetura MVC
- Nome do Projeto: D.I.V.E
- Descrição: D.I.V.E é uma aplicação web que tem como principal objetivo concentrar todos os manuais de montagem da empresa Dell Technologies em um único lugar, permitindo assim um acesso prático pelos montadores das linhas de produção e um alcance maior nas notificações sobre novas atualizações.
- Arquitetura: MVC (Model-View-Controller)
- Ferramenta de Diagramação: Draw.io, Sails.js e Node.js


______


## Modelos (Models):


### Entidades


#### Funcionários


##### Atributos:


- **Id**: Identificador único do funcionário (chave primária);
- **Nome**: Nome completo do usuário;
- **Email**: Email corporativo do usuário;
- **Senha**: Senha de acesso ao sistema fornecida ao usuário;
- **Permissão**: Permissão atribuída ao usuário (montador ou administrador);


#### Manuais


##### Atributos:


- **Id**: Identificador único do manual (chave primária);
- **Título**: Nome do dispositivo;
- **Descrição**: Data de atualização e informações sobre o dispositivo;
- **Conteúdo**: Links, PDFs e modelos 3D associados ao manual;
- **Versão**: Número correspondente a versão mais atual do manual (Ex.: V.1);


### Relações


#### Funcionários <=> Manuais
- Cada funcionário pode ter muitos manuais atribuídos a ele
- Cada manual pode ser atribuído para muitas pessoas
- Relação de muitos para muitos


______


### Controladores (Controllers):

#### Controle de usuário
- Responsável pela autenticação de usuário e autorização de acesso;
- Ações:
    - Autenticação(email, senha)
        - **Parâmetros de entrada:** email (string), senha (string)
        - **Parâmetros de saída:** permissão (administrador ou funcionário)
        - Interage com o modelo Funcionários para verificar se o usuário forneceu as credenciais corretas e qual seu respectivo nível de acesso;
        - Retorna o objeto User autenticado ou null se as credenciais forem inválidas.

#### Interações com os manuais
- Responsável pela adição, atualização, visualização e listagem dos manuais
- Ações:
    - Adicionar()
        - **Parâmetro de entrada:** Nome do dispositivo, descrição, conteúdo
        - Envia para o banco de dados as informações e arquivos necessários para criar um novo manual;
    - Atualizar(Id, novadescrição, novosconteúdos, novaversão)
        - **Parâmetro de entrada:** Id do manual, novadescrição (Caso necessário), novosconteúdos (Caso necessário), novaversão;
        - Envia para o banco de dados novas informações que devem sobrescrever as antigas a fim de atualizar o manual;
    - Visualizar(Id, nomedoDispositivo, descrição, versão, conteúdo)
        - **Parâmetro de entrada:** Id do manual
        - **Parâmetro de saída:** Nome do dispositivo, descrição, versão e conteúdo
        - Envia para o banco de dados o Id do manual e retorna todo conteúdo que está atrelado a ele;
    - Listar(nomedoDispositivo, descrição, versão, conteúdo)
        - **Parâmetro de saída:** Nome, descrição, versão e conteúdo de todos os dispositivos no banco de dados;
        - Recebe do banco de dados todas as informações sobre todos os dispositivos armazenados;
______

### Views (Views):
- **Login**: Permite o usuário fazer login na aplicação;
- **Homepage Admin**: Permite o administrador adicionar, remover e atualizar manuais existentes;
- **Homepage Funcionário**: Permite o funcionário ler manuais, saber quais foram atualizados e suas respectivas versões;
- **Tela de Manuais**: Recebe as informações dos manuais e as organiza de forma visual para o usuário;

______

### Infraestrutura:

#### Banco de dados
- Para o banco de dados foi escolhido o PostgreSQL já que precisamos de um banco de dados relacional que nos permitisse armazenar usuários, senhas, manuais e arquivos de forma eficiente.
- Ele se relaciona com o MVC por meio dos controllers que enviam comandos e retornam as informações necessárias presentes no banco de dados.

#### Autenticação e Autorização:

- Para a autenticação e autorização foi escolhido o sistema SSO, um serviço de autenticação responsável pelo login dos usuários.
- Os controllers de usuário podem integrar-se com o serviço de autenticação para verificar as credenciais do usuário durante o login e controlar o acesso às funcionalidades da aplicação.
_____

### Implicações da Arquitetura:
#### Manutenção
- A utilização da arquitetura MVC permite uma compreensão eficiente dos processos que envolvem a aplicação, essa compreensão facilita a manutenção do código e das relações do serviço
- Testar o código, realizar manutenções e implementar processos de controle de versão são boas práticas essenciais para manter a estabilidade do sistema ao longo do tempo.

______

### Recursos Adicionais:
Documentação do Sails.js: https://github.com/balderdashy/sails
Tutorial do draw.io: https://m.youtube.com/watch?v=w3zm-wbmlpc
