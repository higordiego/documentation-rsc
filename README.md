# Documentação de git-flow - RSC

Esse documento pretende estabelecer um passo-a-passo comum à ser seguido por todos os desenvolvedores para que possamos minimizar os problemas de conflitos de merge, “lock” nas branches nos ambientes e etc…
Será simulado o processo completo de alguém que irá desenvolver uma feature (inovação/sustentação) dentro de um repositório já existente, já que esse é o cenário mais comum.


# Entendendo as branches
Foi definido que em um cenário comum, o repositório de um projeto terá 3 branches principais (variações poderão ocorrer de acordo com a necessidade ou limitações do projeto):
 - **Master**: essa branch se destina somente à versão do projeto que está em produção, já tendo passado pelo desenvolvimento, Q.A e Homologação do cliente.
 - **Homolog**: nesta branch, estará a versão que está sendo homologada pelo cliente, ou seja, última etapa antes de ir para produção.
 - **Development**: aqui estará a versão mais recente do projeto, com todas as features recém desenvolvidas que ainda estão passando pelos testes de Q.A. Ou seja, aqui estarão as features que o cliente solicitou, mas que ainda não estão disponível para homologação.

 Porém, lembre-se de que **não se deve realizar alterações diretamente nestas branches**, salvo em casos de **urgência** e com a **aprovação** do gestor. Para o desenvolvimento de manutenções e novas features, deverá ser criada novas branches, baseadas na branch **‘homolog’**, com o código da ficha do **Azure** que se referem a aquele desenvolvimento, para a realização do merge posteriormente, como será demonstrado a seguir.


## Passo-a-passo do processo de desenvolvimento
Para a demonstração do fluxo do processo de desenvolvimento, vamos tomar como exemplo o projeto fictício **‘XXX-dddd’** . Este projeto possui um único arquivo **‘index.js’**, e ainda não possui versão em produção (Caso deseje criar o estado inicial do repositório para seguir os exemplos deste documento, execute o passo a passo descrito no Apêndice A).

O estado inicial do projeto, por tanto, encontra-se da seguinte forma:

  - Branch master: **vazia**
  - Arquivo **index.js** na branch **homolog** (versão sendo atualmente homologada pelo cliente):
  ```Imagem aqui```
  - Arquivo index.js na branch **development** (versão sendo atualmente testada pelo Q.A):
  ```Imagem aqui```

## Iniciando o desenvolvimento de uma nova demanda

Você, como desenvolvedor, acaba de receber uma nova demanda de manutenção solicitada pelo cliente. A história no azure possui o código XXX-dddd-001. Partindo do pressuposto que o repositório do projeto encontra-se em seu computador, com as 3 branches principais **(master, homolog e development)** atualizadas, você está pronto para iniciar o fluxo de desenvolvimento (Caso ainda não possua o repositório do projeto clonado em seu computador, consulte o passo 3 do Apêndice A. Caso possua o repositório clonado, mas as branches principais estejam desatualizadas, consulte o Apêndice B para mais informações de como atualizar uma branche local).

Dentro da pasta raiz do repositório local, certifique-se de que você está dentro da branch homolog com o comando ‘git status’. Caso não esteja, rode o comando ‘git checkout homolog’ para navegar até a branch homolog.



```Imagem aqui```



Dentro da branch homolog, crie uma nova branch com o código da ficha do Jira com o comando ‘git checkout -b XXX-dddd-001’.