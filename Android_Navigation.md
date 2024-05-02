**Navigation**

O conceito básico de navegação e que temos uma pilha de tela e a media que vamos navegando pelo aplicativos adicionando uma View a pilha, e quando retornamos tiramos a View do topo da pilha. A Tela inicial do seu aplicativo será a mesma que a final

* **Criação de NavGraph**
  
  * **Compose**
    
    *Irei Complementar Depois quando tiver trabalhando diretamente com o compose *
  
  * **Fragment**
    
    * DSL
      
      * Primeiro, é necessário criar a `NavHostFragment`, que *não* pode incluir um elemento `app:navGraph`:
        
        ![](C:\Users\João%20Lucas\AppData\Roaming\marktext\images\2024-05-02-12-44-05-image.png)
      
      * Em seguida, transmita o *i*`id` do `NavHostFragment` para `NavController.findNavController()`. Isso associa o NavController ao `NavHostFragment`.
      
      * Em seguida, a chamada para `NavController.createGraph()` vincula o gráfico ao `NavController` e, consequentemente, também ao `NavHostFragment`: ![](C:\Users\João%20Lucas\AppData\Roaming\marktext\images\2024-05-02-12-42-57-image.png)
    
    * XML
      
      1. Assim como usamos no nosso app Ouite, Criar um `NavHostFragment` contém o atributo `app:navGraph`
         
         ![](C:\Users\João%20Lucas\AppData\Roaming\marktext\images\2024-05-02-12-43-31-image.png)
         
         No nav_graph![](C:\Users\João%20Lucas\AppData\Roaming\marktext\images\2024-05-02-12-46-52-image.png)        

* **Dialogs**
  
  * Compose == DSL
    
    Dentro do escopo aberto para `.createGraph` como um fragment passamos a o dialog
    
    ![](C:\Users\João%20Lucas\AppData\Roaming\marktext\images\2024-05-02-12-48-14-image.png)
  
  * XML
    
    No *xml* dento do arquivo nav_graph, e invés de passar a tag `<fragment>` passa a tag `<dialog>`

* **Activity**

* **Graficos Aninhados**

* **Link Direto**
  
  * **Processar Links Diretos**


