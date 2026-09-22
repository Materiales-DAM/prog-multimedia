---
cover: ../../../../.gitbook/assets/image (5).png
coverY: 227.81866666666667
layout:
  width: default
  cover:
    visible: true
    size: hero
    mask: none
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# Implementación de los viewmodel

Cuando usamos esta arquitectura, los viewmodel cargan como dependencias los use cases que va a utilizar la ventana a la que están vinculados.

Siguiendo el ejemplo de la ventana de usuarios tendríamos el siguiente ViewModel

<pre class="language-kotlin"><code class="lang-kotlin">import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import kotlinx.coroutines.flow.SharingStarted
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.flow.stateIn
import kotlinx.coroutines.launch

class UsersScreenViewModel(
<strong>    private val getUsersUseCase: GetUsersUseCase,
</strong><strong>    private val deleteUserUseCase: DeleteUserUseCase
</strong>) : ViewModel() {

    // La lista de usuarios se carga usando el getUsersUseCase
<strong>    private var _users = getUsersUseCase()
</strong><strong>        .stateIn(viewModelScope, SharingStarted.WhileSubscribed(5000), emptyList())
</strong>
    val users: StateFlow&#x3C;List&#x3C;User>> = _users

    fun removeProduct(id: String) {
        viewModelScope.launch {
            // Invoca el deleteUserUseCase
<strong>            deleteUserUseCase(id)
</strong>        }
    }
}
</code></pre>
