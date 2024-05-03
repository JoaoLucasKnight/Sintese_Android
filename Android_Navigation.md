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



## Usar NavGraph

    Após criado o `NavGraph` o `NavController` está disponível para uso. A unica função disponivel para navegar é a `<u>NavController.navigate()</u>`

- Podendo receber uma route (Melhor maneira)

- Podendo receber um ID
  
  ```kotlin
  navController.navigate("friendslist")
  
  navController.navigate(R.id."id_da_view)
  ```



**Navegar Com Opções**

    Quando utiliza a DSL gera uma class `NavAction` (Destino, 'Bundle', e 'NavOptions')

**XML:** Dentro da tag action passa as informações

</fragment>

**Programatica:** dessa forma substitui todas configurações do xml

```kotlin
findNavController().navigate(R.id.action_fragmentOne_to_fragmentTwo,
    null,navOptions { // Use the Kotlin DSL for building NavOptions
        anim {
            enter = android.R.animator.fade_in
            exit = android.R.animator.fade_out
        }
    }
)
```

**Transmitir dados com Bundle**

- Cria um objeto bundle e passa ele pro destino com o `navigate()`

        `val bundle = bundleOf("amount" to amount)`

        `view.findNavController().navigate(R.id.confirmationAction, bundle)`

- Recupera no destino com `getArguments()`

```kotlin
val tv = view.findViewById<TextView>(R.id.textViewAmount)

tv.text = arguments?.getString("amount")
```

**Safe Args -** Permite a navegação segura de tipo entre destino

    Caso você esteja utilizando o 'Gradle', e não esteja utilizando o 'Compose'

[Safe Args (passo a passo)](https://developer.android.com/guide/navigation/use-graph/safe-args?hl=pt-br#enable)

**Animações entre destinos**

    *Completar*

**Navegação condicional**

    Usado quando existe uma bifurcação, ou seja quando dependendo de uma ação a tela a qual se segue a navegação será diferente

    *Completar*

## BackStack

**Pilha de execução**

- Destino

- adiciona na pilha `NavController().navigate()`

- Remove da pilha `NavController().navigateUp()` e `NavController().popBackStack()`     *a diferença que o navigateUp não sai do app, e o outro sim*

- `popUpTo` ("id" ou "route")retorna a um destino de backStack e limpa

- `Inclusive` ("Boolean") remove até o destino

- `saveState` salvar o estado do destinos retirados da pilha



**Dialogs :** Os *Dialogs* só podem existir no topo da lista de execução. Pode ter um *Dialog* em cima de outro. Mas no momento que o destino não ser um outro *dialogs* . Todos os *dialogs* são removidos da BackStack



**Varias BackStacks**

*Completar*

## Integração

Nesta parte e as formas que pode integrar o *navigation* com outros recurso

- modulo de recurso : Baixar algo quando necessário, para maior compatibilidades com aparelhos com menos capacidade

- Conectar com componentes da interface
