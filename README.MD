# Dropbox clone com JavaScript e Firebase

![Interface do Dropbox Clone](https://firebasestorage.googleapis.com/v0/b/repository-c12c5.appspot.com/o/Capa%20projeto%20Dropbox%20Clone.png?alt=media&token=c4581b15-58b4-4b77-b32b-fbac5235c466 "Interface do Dropbox Clone")

Clone do Dropbox desenvolvido com JavaScript e Firebase. Este projeto foi desenvolvido durante o curso completo de JavaScript da [Hcode](https://hcode.com.br/ "Hcode") e permite realizar o upload de arquivos tanto para um servidor local como para o Firebase Storage.

## Funcionalidades disponíveis

Este aplicativo possui as seguintes funcionalidades:
- Upload de arquivos tanto em servidor local como no Firebase Storage (por padrão usa o Storage, porém você pode descomentar as linhas de upload do servidor local).
- Barra de carregamento mostrando o progresso do upload
- Criar pastar na nuvem
- Renomear arquivos e pastas
- Seleção de múltiplos arquivos
- Exclusão de um ou mais arquivos
- Exclusão de pastas
- Navegação entre diretórios via barra de caminho

## Como funciona ?

O aplicativo faz o upload de arquivos para o Firebase Storage ou servidor local. Os metadados desses arquivos são salvos no Firebase Realtime Database e usados para recuperar informações de nome, diretório, ícone e URL de download. A hierarquia de pastas é criada de forma virtual por meio de coleções no Realtime Database, assim a pasta "*Minhas Fotos*" nada mais é do que uma coleção contendo os metadados dos arquivos, que em tese estão dentro desta pasta. Os metadados das pastas também são armazenados como registros no banco, para que seja possível linka-las as coleções. Ao abrir um diretório, o app lê os registros da coleção vinculada aquela pasta e exibe os arquivos na tela.  O caminho de arquivos é controlado por uma estrutura de vetor que armazena a hierarquia das pastas.

## Recursos utilizados

O projeto utiliza dos seguintes serviços do [Firebase](https://firebase.google.com/?hl=pt "Firebase"):
1. *Storage* - para armazenamento de arquivos
2. *Realtime Database* - Criação da hierarquia virtual de diretórios e armazenamento de metadados.

O aplicativo também usa o [bower](https://bower.io/ "bower") como gerenciador das dependências Front-End.

## Melhorias e correções

O projeto da Hcode apresentava problemas nas funções de renomear e excluir pastas ou arquivos. Isso acontecia porque ao renomear esses itens, a referência original era perdida, fazendo com que uma pasta apontasse para uma coleção não existente e um arquivo deixasse de ser exibido corretamente. Como as referências não estavam corretas, tentar excluir esses itens gerava sucessivos erros na aplicação. A solução desse problema foi implementada por meio de um nome virtual. Sempre que o usuário renomeia um item, ele altera o nome virtual e não o nome real, de modo que ainda será possível linkar os metadados as suas coleções e arquivos.
Para incrementar as funcionalidades da aplicação foram adicionados eventos de teclado as opções de renomear e excluir. A tecla F2 permite renomear arquivos ou pastas, enquanto a tecla DEL está atrelada a exclusão de um ou mais itens. Para evitar exclusões acidentais foi implementada uma tela de confirmação antes da operação.

## Instalação 

A instalação do projeto é muito fácil. Precisaremos do Bower para restaurar as dependências do Front-End. Caso não o tenha instalado, você pode fazê-lo com o seguinte comando:

`npm install -g bower`

Para restaurar as dependências Front-End acesse a pasta public e dentro dela execute o comando abaixo:

`bower install`

Após isso, volte para o diretório principal e restaure as dependências do Back-End com o comando:

`npm install`

Instaladas as dependências, você pode executar a aplicação com o comando abaixo. Ele subirá o app no endereço localhost:3000.

`npm start`