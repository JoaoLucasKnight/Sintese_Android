**Navigation**

O conceito básico de navegação e que temos uma pilha de tela e a media que vamos navegando pelo aplicativos adicionando uma View a pilha, e quando retornamos tiramos a View do topo da pilha. A Tela inicial do seu aplicativo será a mesma que a final

**Criação de NavGraph**

* **Compose**
  
  *Irei Complementar Depois quando tiver trabalhando diretamente com o compose *

* **Fragment**
  
  * DSL
    
    * Primeiro, é necessário criar a `NavHostFragment`, que *não* pode incluir um elemento `app:navGraph`:
      
      ```xml
      <FrameLayout 
      xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto"    
      android:layout_width="match_parent"    
      android:layout_height="match_parent">    
      
      <androidx.fragment.app.FragmentContainerView        
      android:id="@+id/nav_host_fragment"        
      android:name="androidx.navigation.fragment.NavHostFragment"
      android:layout_width="match_parent"        
      android:layout_height="match_parent" />
          
      </FrameLayout>
      ```
    
    * Em seguida, transmita o *i*`id` do `NavHostFragment` para `NavController.findNavController()`. Isso associa o NavController ao `NavHostFragment`.
    
    * Em seguida, a chamada para `NavController.createGraph()` vincula o gráfico ao `NavController` e, consequentemente, também ao `NavHostFragment`: 
      
      ```kotlin
      // Retrieve the NavController.
      
      val navController = findNavController(R.id.nav_host_fragment)
      
      // Add the graph to the NavController with `createGraph()`.
      navController.graph = navController.createGraph(    
          startDestination = "profile") {    
      // Associate each destination with one of the route constants. 
         fragment<ProfileFragment>("profile") {        
              label = "Profile"
          }  
        
          fragment<FriendsListFragment>("friendsList") {
              label = "Friends List"
          }    
      // Add other fragment destinations similarly.
      }
      ```
  
  * XML
    
    1. Assim como usamos no nosso app Ouite, Criar um `NavHostFragment` contém o atributo `app:navGraph`
       
       ![](C:\Users\João%20Lucas\AppData\Roaming\marktext\images\2024-05-02-12-43-31-image.png)
       
       No nav_graph
       
       ```xml
       <FrameLayout 
           xmlns:android="http://schemas.android.com/apk/res/android"
           xmlns:app="http://schemas.android.com/apk/res-auto"
           android:layout_width="match_parent"
           android:layout_height="match_parent">
       
           <androidx.fragment.app.FragmentContainerView
               android:id="@+id/nav_host_fragment"
               android:name="androidx.navigation.fragment.NavHostFragment"
               android:layout_width="match_parent"
               android:layout_height="match_parent"
               app:navGraph="@navigation/nav_graph"/>
           
       </FrameLayout>
       ```

**Dialogs**

* Compose == DSL
  
  Dentro do escopo aberto para `.createGraph` como um fragment passamos a o dialog
  
  ```kotlin
  // Add the graph to the NavController with `createGraph()`.
  navController.graph = navController.createGraph(
      startDestination = "home"
  ) {    
      // Associate the "home" destination with the HomeFragment.
      fragment<HomeFragment>("home") {
          label = "Home"
      }
  
      // Define the "settings" destination as a dialog using DialogFragment.
      dialog<SettingsDialogFragment>("settings") {
          label = "Settings Dialog"    
  }
  ```

* XML
  
  No *xml* dento do arquivo nav_graph, e invés de passar a tag `<fragment>` passa a tag `<dialog>`

**Activity**

Por padão a o NavController é anexado em um layout Activity, ou seja se um usuario ir para outra `Activity` saira do escopo do Graph

*Aplicar no proximo app*

<?xml version="1.0" encoding="utf-8"?>

<div>
  
<navigation 
xmlns:android="http://schemas.android.com/apk/res/android"    
xmlns:app="http://schemas.android.com/apk/res-auto"    
android:id="@+id/navigation_graph"    
app:startDestination="@id/simpleFragment">    
    <activity        
    android:id="@+id/sampleActivityDestination"        
    android:name="com.example.android.navigation.activity.DestinationActivity"**        
    android:label="@string/sampleActivityTitle" /> 
</navigation> 
</div>

* **Graficos Aninhados**
  
  Gráficos aninhandos são duas ou mais estrutura de gráfico, são uteis quando voce precisa de mais de uma tela de origem. Por exemplo: temos o nosso graph principal de tela inicial e temos um graph de configuração. Quando entramo no graph de configuração a tela inicial será a tela de configuração, apenas quando vc tiver na tela inicial de configuração você vai poder voltar pra o graph principal
  
  ![](C:\Users\João%20Lucas\AppData\Roaming\marktext\images\2024-05-02-13-11-47-image.png)
  
  **Compose/DSL**
  
  ![](C:\Users\João%20Lucas\AppData\Roaming\marktext\images\2024-05-02-13-12-23-image.png)
  
  xml: Você abre uma nova tag navigation dentro da outra com seus atributos.passando para o *findaNavController().navigate(*" id do navigation "*)*

* **Link Direto**
  
  * **Processar Links Diretos**


