# Documentação de git-flow - RSC.

Esse documento pretende estabelecer um passo-a-passo comum à ser seguido por todos os desenvolvedores para que possamos minimizar os problemas de conflitos de merge, “lock” nas branches nos ambientes e etc…
Será simulado o processo completo de alguém que irá desenvolver uma feature (inovação/sustentação) dentro de um repositório já existente, já que esse é o cenário mais comum.


# Entendendo as branches.

Foi definido que em um cenário comum, o repositório de um projeto terá 3 branches principais (variações poderão ocorrer de acordo com a necessidade ou limitações do projeto):
 - **Master**: essa branch se destina somente à versão do projeto que está em produção, já tendo passado pelo desenvolvimento, Q.A e Homologação do cliente.
 - **Homolog**: nesta branch, estará a versão que está sendo homologada pelo cliente, ou seja, última etapa antes de ir para produção.
 - **Development**: aqui estará a versão mais recente do projeto, com todas as features recém desenvolvidas que ainda estão passando pelos testes de Q.A. Ou seja, aqui estarão as features que o cliente solicitou, mas que ainda não estão disponível para homologação.

 Porém, lembre-se de que **não se deve realizar alterações diretamente nestas branches**, salvo em casos de **urgência** e com a **aprovação** do gestor. Para o desenvolvimento de manutenções e novas features, deverá ser criada novas branches, baseadas na branch **‘homolog’**, com o código da ficha do **Azure** que se referem a aquele desenvolvimento, para a realização do merge posteriormente, como será demonstrado a seguir.


## Passo-a-passo do processo de desenvolvimento.

Para a demonstração do fluxo do processo de desenvolvimento, vamos tomar como exemplo o projeto fictício **‘XXX-dddd’** . Este projeto possui um único arquivo **‘index.js’**, e ainda não possui versão em produção (Caso deseje criar o estado inicial do repositório para seguir os exemplos deste documento, execute o passo a passo descrito no Apêndice A).

O estado inicial do projeto, por tanto, encontra-se da seguinte forma:

  - Branch master: **vazia**
  - Arquivo **index.js** na branch **homolog** (versão sendo atualmente homologada pelo cliente):
  ```Imagem aqui```
  - Arquivo index.js na branch **development** (versão sendo atualmente testada pelo Q.A):
  ```Imagem aqui```

## Iniciando o desenvolvimento de uma nova demanda.

Você, como desenvolvedor, acaba de receber uma nova demanda de manutenção solicitada pelo cliente. A história no azure possui o código XXX-dddd-001. Partindo do pressuposto que o repositório do projeto encontra-se em seu computador, com as 3 branches principais **(master, homolog e development)** atualizadas, você está pronto para iniciar o fluxo de desenvolvimento (Caso ainda não possua o repositório do projeto clonado em seu computador, consulte o passo 3 do Apêndice A. Caso possua o repositório clonado, mas as branches principais estejam desatualizadas, consulte o Apêndice B para mais informações de como atualizar uma branche local).

Dentro da pasta raiz do repositório local, certifique-se de que você está dentro da branch homolog com o comando ‘git status’. Caso não esteja, rode o comando ‘git checkout homolog’ para navegar até a branch homolog.

```Imagem aqui```

Dentro da branch homolog, crie uma nova branch com o código da ficha do Jira com o comando **‘git checkout -b XXX-dddd-001’**.

```imagem aqui```

**Lembre-se**: Em uma situação normal, sempre faremos o desenvolvimento de uma manutenção ou nova feature baseada na branch homolog, pois a branch master tende a ser muito defasada em relação a homolog, e a branch development tende a ser muito instável uma vez que outras features estão sendo testadas pelo Q.A e pode sofrer mudanças com uma alta frequência. Além disso, utilizamos o código da ficha do Jira como nome da branch para fins de rastreabilidade e auditoria. 


## Aplicando as correções necessárias.

Certifique-se de estar dentro da branch XXX-dddd-001 com o comando **‘git status’**. Abra o seu editor de código e inicie a correção solicitada, realizando todos os testes necessários de forma local. Para exemplificar, considere que foram realizadas as seguintes alterações no arquivo index.js:

```imagem aqui ```

Quando as modificações necessárias para a manutenção forem concluídas, é hora de fazer o commit. **Lembre-se**: evite de acumular muitas alterações em um único commit pois isso dificulta a rastreabilidade das alterações do projeto.

Ainda dentro da branch XXX-dddd-001, rode o comando **‘git status’** e note que os arquivos com alterações pendentes de commit serão listados:

```imagem aqui ```

Para confirmar as alterações, rode o comando **‘git add .’** (note que o ponto faz parte do comando. Ele indica que deverá ser adicionado todos os arquivos modificados). Para confirmar que o comando anterior funcionou, rode novamente o comando o **‘git status’**.

```imagem aqui ```

 Por fim, realize o commit da modificação realizada com o comando **‘git commit -m “<comentário_da_alteração>”’**, seguido da atualização do repositório remoto com **‘git push origin XXX-dddd-001’**.

 ```imagem aqui ```


## Disponibilizando as alterações para testes do Q.A.

Uma vez tendo finalizado as modificações necessárias, é hora de disponibilizar suas correções para o ambiente de teste do Q.A, ou seja, passar as alterações realizadas para a branch ‘development’. Realize a seguinte sequência de passos:

- Atualize a sua branch XXX-dddd-001 com os commits da branch homolog. Assim, caso a branch homolog tenha sido atualizada por outro desenvolvedor durante o seu desenvolvimento, garantimos que todas as alterações já testadas pelo Q.A continuarão presentes. **Dentro da branch XXX-dddd-001** rode o comando **‘git pull origin homolog’**.

```imagem aqui```

- Atualize a branch ‘development’ local com os commits da própria branch ‘development’ remota. Assim, garantimos que no momento do merge nenhum commit anterior ficará de fora. **Dentro da branch development**, rode o comando **‘git pull origin development’**.


```imagem aqui```

- Por fim, ainda **dentro da branch ‘development’**, rode o comando **‘git merge XXX-dddd-001’**.



