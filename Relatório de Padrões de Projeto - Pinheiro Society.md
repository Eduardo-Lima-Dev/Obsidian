## 1. Introdução
### 1.1 Contexto do Projeto
O **Pinheiro Society** é um sistema completo de gestão para estabelecimentos esportivos desenvolvido em Flutter/Dart para a plataforma Desktop. O sistema oferece funcionalidades de reservas de quadras, comandas, controle de estoque, gestão de clientes e relatórios administrativos, integrando-se com uma API REST desenvolvida em Node.js/TypeScript.
### 1.2 Objetivo do Documento
Este documento apresenta um relatório técnico detalhado dos padrões de projeto (Design Patterns) identificados e implementados no código-fonte do projeto Pinheiro Society. Para cada padrão, são documentados:

- **Localização**: Onde o padrão está implementado no código
- **Justificativa**: Por que o padrão foi escolhido e utilizado
- **Problemas Resolvidos**: Quais problemas técnicos e arquiteturais o padrão resolve
- **Detalhes de Implementação**: Como o padrão foi implementado na prática
### 1.3 Metodologia de Identificação
Os padrões foram identificados através de análise estática do código-fonte, revisão da arquitetura do projeto e compreensão dos problemas que cada padrão resolve. A identificação foi baseada em:

- Estrutura de diretórios e organização do código
- Padrões de comunicação entre componentes
- Abstrações e interfaces implementadas
- Uso de bibliotecas e frameworks (Provider, ChangeNotifier)
---
## 2. Padrões Arquiteturais

### 2.1 Repository Pattern
#### 2.1.1 Onde Está Implementado

O padrão Repository está implementado em:

- **Diretório**: `lib/services/repositories/`
- **Arquivos principais**:
- `auth_repository.dart` - Autenticação e gerenciamento de usuários
- `cliente_repository.dart` - Gestão de clientes
- `quadra_repository.dart` - Gestão de quadras
- `mesa_repository.dart` - Gestão de mesas
- `produto_repository.dart` - Gestão de produtos
- `dashboard_repository.dart` - Dados do dashboard
- `relatorio_repository.dart` - Geração de relatórios
- `lancamento_repository.dart` - Lançamentos financeiros

#### 2.1.2 Por Que Foi Utilizado

  

O Repository Pattern foi escolhido para:

  

1. **Abstração da Camada de Dados**: Isola completamente a lógica de acesso a dados (API HTTP) do restante da aplicação, criando uma camada de abstração clara.

  

2. **Facilidade de Testes**: Permite criar mocks dos repositórios para testar controllers e lógica de negócio sem depender de chamadas reais à API.

  

3. **Manutenibilidade**: Centraliza toda a lógica de comunicação HTTP em um único local, facilitando manutenção e evolução do código.

  

4. **Flexibilidade**: Permite trocar a implementação da fonte de dados (API REST, GraphQL, banco local) sem afetar os controllers e a UI.

  

5. **Reutilização**: Métodos de repositório podem ser reutilizados em diferentes controllers, evitando duplicação de código.

  

#### 2.1.3 Problemas que Resolve

  

O padrão Repository resolve os seguintes problemas:

  

1. **Acoplamento Direto UI-API**: Sem o padrão, widgets e controllers precisariam conhecer detalhes de implementação HTTP (URLs, headers, métodos), criando acoplamento forte.

  

2. **Duplicação de Código**: Lógica de requisições HTTP seria repetida em múltiplos lugares, dificultando manutenção e aumentando risco de inconsistências.

  

3. **Dificuldade para Testar**: Testar controllers seria difícil sem poder mockar as chamadas à API.

  

4. **Mudanças na API**: Alterações na estrutura da API (endpoints, formato de resposta) afetariam múltiplos pontos do código.

  

5. **Lógica de Negócio Misturada**: Sem separação clara, lógica de negócio ficaria misturada com detalhes de comunicação HTTP.

  

#### 2.1.4 Detalhes da Implementação

  

**Estrutura das Classes Repository:**

  

```dart

class AuthRepository {

static Future<Map<String, dynamic>> login({

required String email,

required String password,

}) async {

return await ApiClient.post('/auth/login', {

'email': email,

'password': password,

});

}

// Outros métodos estáticos...

}

```

  

**Características da Implementação:**

  

- **Classes Estáticas**: Todos os repositórios utilizam métodos estáticos, eliminando necessidade de instanciação e permitindo acesso direto.

  

- **Encapsulamento do ApiClient**: Os repositórios encapsulam chamadas ao `ApiClient`, que por sua vez gerencia headers, autenticação e tratamento de erros.

  

- **Retorno Padronizado**: Todos os métodos retornam `Map<String, dynamic>` com estrutura:

  

```dart

{

'success': bool,

'data': dynamic, // quando success = true

'error': String // quando success = false

}

```

  

- **Métodos Específicos por Operação**: Cada repositório expõe métodos específicos para suas operações (ex: `login()`, `createCliente()`, `updateQuadra()`, `deleteProduto()`).

  

- **Tratamento de Parâmetros**: Métodos recebem parâmetros tipados e estruturados, facilitando uso e validação.

  

**Exemplo de Uso:**

  

```dart

// No controller

final result = await AuthRepository.login(

email: email,

password: password,

);

  

if (result['success']) {

// Processar dados

} else {

// Tratar erro

}

```

  

---

  

### 2.2 MVVM (Model-View-ViewModel)

  

#### 2.2.1 Onde Está Implementado

  

O padrão MVVM está implementado em toda a estrutura do dashboard:

  

- **Models**: `lib/features/dashboard/models/`

- `cliente.dart`, `quadra.dart`, `reserva.dart`, `produto.dart`

- `mesa_aberta.dart`, `item_comanda.dart`, `movimentacao_estoque.dart`

- `dashboard_summary.dart`, `relatorio_faturamento_model.dart`

  

- **Views**:

- `lib/screens/dashboard_screen.dart` - Tela principal

- `lib/features/dashboard/sections/` - Seções do dashboard

- `home_section.dart`, `clientes_section.dart`, `quadras_section.dart`

- `agendamentos_section.dart`, `mesas_section.dart`, `estoque_section.dart`

- `relatorios_section.dart`

  

- **ViewModels (Controllers)**: `lib/features/dashboard/controllers/`

- `dashboard_controller.dart`, `home_controller.dart`

- `clientes_controller.dart`, `quadras_controller.dart`

- `agendamentos_controller.dart`, `mesas_controller.dart`

- `estoque_controller.dart`, `venda_avulsa_controller.dart`

  

#### 2.2.2 Por Que Foi Utilizado

  

O padrão MVVM foi escolhido porque:

  

1. **Separação de Responsabilidades**: Divide claramente a aplicação em três camadas com responsabilidades bem definidas, facilitando compreensão e manutenção.

  

2. **Testabilidade**: Permite testar cada camada isoladamente - models podem ser testados sem UI, controllers podem ser testados sem widgets.

  

3. **Reutilização**: Lógica de negócio nos controllers pode ser reutilizada em diferentes views (ex: mesmo controller para mobile e web).

  

4. **Manutenibilidade**: Mudanças na UI não afetam lógica de negócio e vice-versa, facilitando evolução do sistema.

  

5. **Alinhamento com Flutter**: O padrão MVVM se alinha perfeitamente com a arquitetura recomendada pelo Flutter, utilizando `ChangeNotifier` e `Provider`.

  

#### 2.2.3 Problemas que Resolve

  

O padrão MVVM resolve os seguintes problemas:

  

1. **Mistura de Lógica e Apresentação**: Sem separação, lógica de negócio ficaria misturada com código de UI, dificultando manutenção.

  

2. **Dificuldade para Testar**: Testar widgets com lógica embutida é complexo e frágil.

  

3. **Código Difícil de Manter**: Mudanças em regras de negócio exigiriam alterar código de UI, aumentando risco de bugs.

  

4. **Acoplamento Forte**: UI fortemente acoplada a estruturas de dados e lógica, dificultando refatoração.

  

5. **Duplicação de Lógica**: Mesma lógica repetida em múltiplos widgets, causando inconsistências.

  

#### 2.2.4 Detalhes da Implementação

  

**Models (Camada de Dados):**

  

```dart

class Cliente {

final String id;

final String nomeCompleto;

final String cpf;

final String email;

final String telefone;

  

Cliente({

required this.id,

required this.nomeCompleto,

// ...

});

  

factory Cliente.fromJson(Map<String, dynamic> json) {

return Cliente(

id: json['id']?.toString() ?? '',

nomeCompleto: json['nomeCompleto']?.toString() ?? '',

// ...

);

}

  

Map<String, dynamic> toJson() {

return {

'id': id,

'nomeCompleto': nomeCompleto,

// ...

};

}

}

```

  

**Características dos Models:**

- Classes imutáveis com campos `final`

- Construtores `factory fromJson()` para deserialização

- Métodos `toJson()` para serialização

- Métodos `copyWith()` para criar cópias modificadas

  

**ViewModels (Controllers):**

  

```dart

class ClientesController extends ChangeNotifier {

List<Cliente> _clientes = [];

bool _isLoading = false;

String? _error;

  

List<Cliente> get clientes => _clientes;

bool get isLoading => _isLoading;

String? get error => _error;

  

Future<void> carregarClientes() async {

_isLoading = true;

_error = null;

notifyListeners();

  

final result = await ClienteRepository.getClientes();

if (result['success']) {

_clientes = (result['data'] as List)

.map((json) => Cliente.fromJson(json))

.toList();

} else {

_error = result['error'];

}

_isLoading = false;

notifyListeners();

}

}

```

  

**Características dos Controllers:**

- Estendem `ChangeNotifier` para notificar mudanças

- Gerenciam estado da view (dados, loading, erros)

- Encapsulam lógica de negócio e chamadas a repositórios

- Chamam `notifyListeners()` após mudanças de estado

  

**Views (Widgets):**

  

```dart

class ClientesSection extends StatelessWidget {

final ClientesController controller;

  

@override

Widget build(BuildContext context) {

return Consumer<ClientesController>(

builder: (context, controller, child) {

if (controller.isLoading) {

return CircularProgressIndicator();

}

if (controller.error != null) {

return Text('Erro: ${controller.error}');

}

return ListView.builder(

itemCount: controller.clientes.length,

itemBuilder: (context, index) {

return ClienteCard(cliente: controller.clientes[index]);

},

);

},

);

}

}

```

  

**Características das Views:**

- Widgets focados apenas em apresentação

- Usam `Consumer<T>` para observar mudanças nos controllers

- Não contêm lógica de negócio

- Reagem automaticamente a mudanças de estado

  

---

  

### 2.3 Observer Pattern

  

#### 2.3.1 Onde Está Implementado

  

O padrão Observer está implementado em:

  

- **Controllers**: Todos os controllers em `lib/features/dashboard/controllers/` que estendem `ChangeNotifier`

- **Views**: `lib/screens/dashboard_screen.dart` e todas as seções em `lib/features/dashboard/sections/` que utilizam `Consumer` ou `Provider.of`

- **Biblioteca**: Implementado através do pacote `provider` (v6.1.2) e da classe `ChangeNotifier` do Flutter

  

#### 2.3.2 Por Que Foi Utilizado

  

O Observer Pattern foi escolhido porque:

  

1. **Comunicação Reativa**: Permite que componentes reajam automaticamente a mudanças de estado, sem necessidade de polling ou atualização manual.

  

2. **Desacoplamento**: Views não precisam conhecer como ou quando o estado muda, apenas reagem às mudanças.

  

3. **Performance**: Permite atualizações seletivas - apenas widgets que observam mudanças específicas são reconstruídos.

  

4. **Integração Nativa**: O Flutter fornece `ChangeNotifier` e o pacote `Provider` oferece integração perfeita com o framework.

  

5. **Simplicidade**: Reduz complexidade de gerenciamento manual de estado e propagação de eventos.

  

#### 2.3.3 Problemas que Resolve

  

O Observer Pattern resolve os seguintes problemas:

  

1. **Atualização Manual de Widgets**: Sem o padrão, seria necessário chamar `setState()` manualmente em múltiplos lugares após cada mudança de estado.

  

2. **Propagação Manual de Eventos**: Eventos precisariam ser propagados manualmente através de callbacks ou parâmetros, criando acoplamento.

  

3. **Sincronização de Dados**: Dificuldade para manter múltiplos widgets sincronizados com o mesmo estado.

  

4. **Performance com Rebuilds Desnecessários**: Sem observação seletiva, todos os widgets seriam reconstruídos mesmo quando dados não mudaram.

  

5. **Complexidade de Gerenciamento**: Gerenciar estado manualmente aumenta complexidade e risco de bugs.

  

#### 2.3.4 Detalhes da Implementação

  

**Subject (Observable) - Controllers:**

  

```dart

class DashboardController extends ChangeNotifier {

String _selectedSection = 'inicio';

String get selectedSection => _selectedSection;

void selectSection(String section) {

_selectedSection = section;

notifyListeners(); // Notifica todos os observadores

}

}

```

  

**Características:**

- Controllers estendem `ChangeNotifier` (classe do Flutter que implementa o padrão Observer)

- Método `notifyListeners()` notifica todos os observadores registrados

- Estado encapsulado em campos privados com getters públicos

  

**Observer (Widgets que Observam):**

  

```dart

// Usando Consumer

Consumer<DashboardController>(

builder: (context, controller, child) {

return Text('Seção: ${controller.selectedSection}');

},

)

  

// Usando Provider.of

final controller = Provider.of<DashboardController>(context);

```

  

**Características:**

- `Consumer<T>` reconstrói apenas o widget quando o controller notifica mudanças

- `Provider.of<T>` acessa o controller sem reconstruir automaticamente (útil para ações)

- Widgets são automaticamente desinscritos quando removidos da árvore

  

**Registro de Observers (Dependency Injection):**

  

```dart

MultiProvider(

providers: [

ChangeNotifierProvider.value(value: _dashboardController),

ChangeNotifierProvider.value(value: _homeController),

// ...

],

child: DashboardScreen(),

)

```

  

**Fluxo de Comunicação:**

  

1. Controller modifica estado interno

2. Controller chama `notifyListeners()`

3. Provider notifica todos os `Consumer` registrados

4. Widgets observadores são reconstruídos com novo estado

5. UI reflete automaticamente as mudanças

  

**Exemplo Completo:**

  

```dart

// Controller (Subject)

class HomeController extends ChangeNotifier {

int _reservasHoje = 0;

int get reservasHoje => _reservasHoje;

Future<void> carregarDados() async {

// ... carrega dados da API

_reservasHoje = dados['reservasHoje'];

notifyListeners(); // Notifica mudança

}

}

  

// View (Observer)

Consumer<HomeController>(

builder: (context, controller, child) {

return Text('Reservas hoje: ${controller.reservasHoje}');

},

)

```

  

---

  

### 2.4 Singleton Pattern / Static Utility

  

#### 2.4.1 Onde Está Implementado

  

O padrão Singleton/Static Utility está implementado em:

  

- **ApiClient**: `lib/services/api_client.dart` - Classe estática para comunicação HTTP

- **UserStorage**: `lib/services/user_storage.dart` - Classe estática para armazenamento local

  

#### 2.4.2 Por Que Foi Utilizado

  

O padrão foi escolhido porque:

  

1. **Ponto Único de Acesso**: Garante que existe apenas uma instância/configuração para recursos compartilhados (cliente HTTP, armazenamento).

  

2. **Evita Múltiplas Instâncias**: Previne criação acidental de múltiplas instâncias de clientes HTTP, que poderiam causar problemas de conexão e consumo de recursos.

  

3. **Acesso Global Simplificado**: Permite acesso a funcionalidades compartilhadas de qualquer lugar da aplicação sem necessidade de passar dependências.

  

4. **Configuração Centralizada**: Centraliza configurações importantes (URL base, headers padrão) em um único local.

  

5. **Simplicidade**: Elimina necessidade de gerenciar ciclo de vida de instâncias e injeção de dependências para utilitários globais.

  

#### 2.4.3 Problemas que Resolve

  

O padrão resolve os seguintes problemas:

  

1. **Múltiplas Instâncias de Clientes HTTP**: Sem o padrão, cada widget/controller poderia criar seu próprio cliente HTTP, causando:

- Consumo excessivo de recursos

- Dificuldade para gerenciar conexões

- Configurações inconsistentes

  

2. **Configuração Duplicada**: Headers, URLs e outras configurações seriam repetidas em múltiplos lugares, dificultando manutenção.

  

3. **Gerenciamento de Estado Global**: Dificuldade para gerenciar estado compartilhado (ex: token de autenticação) sem um ponto centralizado.

  

4. **Passagem Manual de Dependências**: Sem acesso global, seria necessário passar clientes HTTP e utilitários por toda a árvore de widgets via construtores.

  

5. **Inconsistência de Configuração**: Diferentes partes da aplicação poderiam usar configurações diferentes, causando bugs difíceis de rastrear.

  

#### 2.4.4 Detalhes da Implementação

  

**ApiClient - Cliente HTTP Estático:**

  

```dart

class ApiClient {

static const String baseUrl = 'https://pinheiro-society-api.vercel.app';

static Map<String, String> get _baseHeaders => {

'Content-Type': 'application/json',

'Accept': 'application/json',

};

static Future<Map<String, String>> _getHeaders() async {

final headers = Map<String, String>.from(_baseHeaders);

final token = await UserStorage.getToken();

if (token != null && token.isNotEmpty) {

headers['Authorization'] = 'Bearer $token';

}

return headers;

}

static Future<Map<String, dynamic>> get(String endpoint) async {

final headers = await _getHeaders();

final res = await http.get(

Uri.parse('$baseUrl$endpoint'),

headers: headers,

);

// ... tratamento de resposta

}

static Future<Map<String, dynamic>> post(

String endpoint,

Map<String, dynamic> body,

) async {

// ... implementação

}

}

```

  

**Características do ApiClient:**

- Todos os métodos são `static`, não requerem instanciação

- URL base centralizada e facilmente modificável

- Headers padrão gerenciados automaticamente

- Token de autenticação adicionado automaticamente em todas as requisições

- Tratamento centralizado de erros HTTP e JSON

- Retorno padronizado: `{success: bool, data?: any, error?: string}`

  

**UserStorage - Facade Estático:**

  

```dart

class UserStorage {

static Map<String, dynamic>? _userData;

static Future<void> saveUserData(Map<String, dynamic> userData) async {

_userData = userData;

}

static Future<String?> getToken() async {

return _userData?['token']?.toString();

}

static Future<String> getUserName() async {

if (_userData?['user'] != null) {

final user = _userData!['user'] as Map<String, dynamic>;

return user['name'] ?? 'Usuário';

}

return 'Usuário';

}

static Future<bool> isAdmin() async {

final role = await getUserRole();

return role?.toUpperCase() == 'ADMIN';

}

static Future<void> clearUserData() async {

_userData = null;

}

}

```

  

**Características do UserStorage:**

- Facade estático que abstrai armazenamento local

- Métodos estáticos para todas as operações

- Acesso direto sem necessidade de instanciação

- Encapsula lógica de acesso a dados do usuário (token, nome, role)

- Facilita migração futura para `shared_preferences` ou outro mecanismo

  

**Exemplo de Uso:**

  

```dart

// Em qualquer lugar da aplicação, sem necessidade de injeção

final result = await ApiClient.get('/clientes');

final token = await UserStorage.getToken();

final isAdmin = await UserStorage.isAdmin();

```

  

**Vantagens da Abordagem Estática:**

- Simplicidade: acesso direto sem configuração

- Performance: sem overhead de criação de instâncias

- Consistência: mesma configuração em toda a aplicação

- Facilidade de uso: não requer injeção de dependências

  

**Considerações:**

- Abordagem estática facilita testes (pode ser mockada)

- Centralização facilita manutenção e evolução

- Útil para utilitários que não têm estado mutável complexo

  

---

  

### 2.5 Factory Pattern

  

#### 2.5.1 Onde Está Implementado

  

O Factory Pattern está implementado em:

  

- **Diretório**: `lib/features/dashboard/models/`

- **Arquivos principais**:

- `cliente.dart` - Factory `Cliente.fromJson()`

- `quadra.dart` - Factory `Quadra.fromJson()`

- `reserva.dart` - Factory `Reserva.fromJson()`

- `produto.dart` - Factory `Produto.fromJson()`

- `mesa_aberta.dart` - Factory `MesaAberta.fromJson()`

- `item_comanda.dart` - Factory `ItemComanda.fromJson()`

- Todos os outros models do sistema

  

#### 2.5.2 Por Que Foi Utilizado

  

O Factory Pattern foi escolhido porque:

  

1. **Encapsulamento da Lógica de Criação**: Esconde a complexidade de criar objetos a partir de dados brutos (JSON), centralizando lógica de parsing.

  

2. **Tratamento Centralizado de Erros**: Permite tratar erros de conversão de tipos e valores nulos em um único local.

  

3. **Flexibilidade**: Facilita evolução do formato de dados da API sem afetar código que usa os models.

  

4. **Validação**: Permite validar e transformar dados durante a criação, garantindo objetos válidos.

  

5. **Consistência**: Garante que todos os objetos são criados da mesma forma, evitando inconsistências.

  

#### 2.5.3 Problemas que Resolve

  

O padrão resolve os seguintes problemas:

  

1. **Conversão Manual Repetitiva**: Sem o padrão, conversão de JSON para objetos seria repetida em múltiplos lugares, causando duplicação.

  

2. **Tratamento de Nulos Espalhado**: Lógica para lidar com valores nulos e tipos opcionais estaria espalhada pelo código.

  

3. **Dificuldade para Evoluir Formato**: Mudanças no formato da API exigiriam alterações em múltiplos pontos do código.

  

4. **Código Duplicado de Parsing**: Mesma lógica de parsing repetida para cada uso do model.

  

5. **Falta de Validação**: Sem centralização, validação de dados seria inconsistente ou ausente.

  

#### 2.5.4 Detalhes da Implementação

  

**Estrutura Básica do Factory:**

  

```dart

class Cliente {

final String id;

final String nomeCompleto;

final String cpf;

final String email;

final String telefone;

  

Cliente({

required this.id,

required this.nomeCompleto,

required this.cpf,

required this.email,

required this.telefone,

});

  

// Factory constructor

factory Cliente.fromJson(Map<String, dynamic> json) {

return Cliente(

id: json['id']?.toString() ?? '',

nomeCompleto: json['nomeCompleto']?.toString() ?? '',

cpf: json['cpf']?.toString() ?? '',

email: json['email']?.toString() ?? '',

telefone: json['telefone']?.toString() ?? '',

);

}

  

Map<String, dynamic> toJson() {

return {

'id': id,

'nomeCompleto': nomeCompleto,

'cpf': cpf,

'email': email,

'telefone': telefone,

};

}

}

```

  

**Características da Implementação:**

  

1. **Construtores Factory**: Usam palavra-chave `factory` em vez de `const` ou construtor normal

```dart

factory Cliente.fromJson(Map<String, dynamic> json)

```

  

2. **Tratamento de Tipos**: Converte dinamicamente tipos da API para tipos do Dart

```dart

id: json['id']?.toString() ?? ''

```

  

3. **Valores Padrão**: Usa operador `??` para fornecer valores padrão quando dados são nulos

```dart

nomeCompleto: json['nomeCompleto']?.toString() ?? ''

```

  

4. **Null Safety**: Usa operador `?.` para acesso seguro a propriedades que podem ser nulas

  

5. **Serialização Reversa**: Método `toJson()` para converter objeto de volta para JSON

  

**Exemplo com Tratamento Complexo (Quadra):**

  

```dart

class Quadra {

final int id;

final String nome;

final bool ativa;

  

Quadra({

required this.id,

required this.nome,

required this.ativa,

});

  

factory Quadra.fromMap(Map<String, dynamic> map) {

return Quadra(

id: _parseId(map['id'] ?? map['_id']),

nome: (map['nome'] ?? map['name'] ?? '').toString(),

ativa: _parseAtiva(map['ativa'] ?? map['status']),

);

}

  

static int _parseId(dynamic value) {

if (value is int) return value;

if (value is num) return value.toInt();

if (value is String) {

return int.tryParse(value) ?? value.hashCode;

}

return DateTime.now().millisecondsSinceEpoch;

}

  

static bool _parseAtiva(dynamic value) {

if (value is bool) return value;

if (value is num) return value != 0;

if (value is String) {

final normalized = value.toLowerCase();

return ['true', '1', 'ativo', 'active'].contains(normalized);

}

return false;

}

}

```

  

**Características Avançadas:**

- Métodos auxiliares estáticos para parsing complexo

- Suporte a múltiplos formatos de entrada (flexibilidade)

- Validação e normalização de dados

- Fallbacks robustos para casos extremos

  

**Uso do Factory:**

  

```dart

// No controller ou repositório

final result = await ApiClient.get('/clientes');

if (result['success']) {

final clientes = (result['data'] as List)

.map((json) => Cliente.fromJson(json))

.toList();

}

```

  

**Vantagens da Implementação:**

- **Robustez**: Trata casos extremos (nulos, tipos diferentes)

- **Manutenibilidade**: Lógica de criação em um único local

- **Testabilidade**: Fácil testar criação de objetos

- **Evolução**: Fácil adaptar a mudanças na API

  

---

  

### 2.6 Dependency Injection (DI)

  

#### 2.6.1 Onde Está Implementado

  

O padrão Dependency Injection está implementado em:

  

- **Arquivo principal**: `lib/screens/dashboard_screen.dart`

- **Biblioteca utilizada**: `provider` (v6.1.2) - Pacote oficial do Flutter para injeção de dependências

- **Uso**: Injeção de todos os controllers do dashboard via `MultiProvider`

  

#### 2.6.2 Por Que Foi Utilizado

  

O Dependency Injection foi escolhido porque:

  

1. **Inversão de Controle**: Controllers são fornecidos externamente, não criados internamente pelos widgets que os usam.

  

2. **Facilita Testes**: Permite injetar mocks dos controllers em testes, facilitando testes unitários e de integração.

  

3. **Reduz Acoplamento**: Widgets não precisam conhecer como criar ou configurar controllers, apenas como usá-los.

  

4. **Compartilhamento de Instâncias**: Permite que múltiplos widgets compartilhem a mesma instância de um controller.

  

5. **Gerenciamento de Ciclo de Vida**: O Provider gerencia automaticamente o ciclo de vida dos controllers (criação, disposição).

  

#### 2.6.3 Problemas que Resolve

  

O padrão resolve os seguintes problemas:

  

1. **Instanciação Manual**: Sem DI, cada widget precisaria criar seus próprios controllers, causando:

- Múltiplas instâncias do mesmo controller

- Dificuldade para compartilhar estado

- Gerenciamento manual de ciclo de vida

  

2. **Dificuldade para Testar**: Substituir controllers por mocks em testes seria difícil sem injeção.

  

3. **Acoplamento Forte**: Widgets fortemente acoplados à criação de dependências, dificultando refatoração.

  

4. **Passagem Manual**: Dependências precisariam ser passadas manualmente por toda a árvore de widgets via construtores.

  

5. **Gerenciamento de Estado**: Dificuldade para gerenciar estado compartilhado entre múltiplos widgets.

  

#### 2.6.4 Detalhes da Implementação

  

**Configuração do MultiProvider:**

  

```dart

class _DashboardScreenState extends State<DashboardScreen> {

late DashboardController _dashboardController;

late HomeController _homeController;

late ClientesController _clientesController;

// ... outros controllers

  

@override

void initState() {

super.initState();

// Criar instâncias dos controllers

_dashboardController = DashboardController();

_homeController = HomeController();

_clientesController = ClientesController();

// ... inicializar outros controllers

}

  

@override

Widget build(BuildContext context) {

return MultiProvider(

providers: [

ChangeNotifierProvider.value(value: _dashboardController),

ChangeNotifierProvider.value(value: _homeController),

ChangeNotifierProvider.value(value: _clientesController),

ChangeNotifierProvider.value(value: _agendamentosController),

ChangeNotifierProvider.value(value: _quadrasController),

ChangeNotifierProvider.value(value: _mesasController),

ChangeNotifierProvider.value(value: _estoqueController),

],

child: Scaffold(

// ... resto da UI

),

);

}

}

```

  

**Características da Implementação:**

  

1. **MultiProvider**: Injeta múltiplos providers na árvore de widgets de uma vez

2. **ChangeNotifierProvider.value**: Usa instâncias já criadas (útil quando precisa controlar ciclo de vida manualmente)

3. **Acesso Global**: Qualquer widget filho pode acessar os controllers injetados

  

**Acesso às Dependências Injetadas:**

  

```dart

// Método 1: Consumer (reconstrói quando há mudanças)

Consumer<DashboardController>(

builder: (context, controller, child) {

return Text('Seção: ${controller.selectedSection}');

},

)

  

// Método 2: Provider.of (acesso direto, sem reconstrução automática)

final controller = Provider.of<DashboardController>(context);

controller.selectSection('clientes');

  

// Método 3: Provider.of com listen: false (otimização)

final controller = Provider.of<DashboardController>(context, listen: false);

```

  

**Exemplo de Uso em Widget Filho:**

  

```dart

class HomeSection extends StatelessWidget {

final HomeController controller;

  

const HomeSection({required this.controller});

  

@override

Widget build(BuildContext context) {

// Controller já foi injetado e passado como parâmetro

// Ou pode ser acessado via Provider.of<HomeController>(context)

return Consumer<HomeController>(

builder: (context, controller, child) {

if (controller.isLoading) {

return CircularProgressIndicator();

}

return DashboardContent(data: controller.summary);

},

);

}

}

```

  

**Vantagens da Abordagem:**

  

1. **Controle de Ciclo de Vida**: Instâncias são criadas em `initState()` e dispostas em `dispose()`

2. **Compartilhamento**: Mesma instância compartilhada por múltiplos widgets

3. **Testabilidade**: Fácil substituir por mocks em testes

4. **Desacoplamento**: Widgets não conhecem detalhes de criação

  

**Gerenciamento de Disposição:**

  

```dart

@override

void dispose() {

_dashboardController.dispose();

_homeController.dispose();

_clientesController.dispose();

// ... dispor outros controllers

super.dispose();

}

```

  

**Fluxo de Injeção:**

  

1. `DashboardScreen` cria instâncias dos controllers

2. `MultiProvider` registra controllers na árvore de widgets

3. Widgets filhos acessam via `Provider.of` ou `Consumer`

4. Provider gerencia acesso e notificações

5. Controllers são dispostos quando `DashboardScreen` é removido

  

---

  

### 2.7 Adapter Pattern

  

#### 2.7.1 Onde Está Implementado

  

O padrão Adapter está implementado em:

  

- **Arquivo**: `lib/services/api_client.dart`

- **Biblioteca adaptada**: `http` (v1.1.0) - Cliente HTTP genérico do Dart

- **Interface adaptada**: Interface específica do domínio Pinheiro Society

  

#### 2.7.2 Por Que Foi Utilizado

  

O Adapter Pattern foi escolhido porque:

  

1. **Adaptação de Interface**: A biblioteca `http` fornece interface genérica que não atende completamente às necessidades específicas do projeto.

  

2. **Padronização**: Permite padronizar formato de respostas e tratamento de erros em toda a aplicação.

  

3. **Abstração de Detalhes**: Esconde detalhes de implementação HTTP (headers, parsing JSON, tratamento de erros) do restante da aplicação.

  

4. **Funcionalidades Específicas**: Adiciona funcionalidades específicas do domínio (autenticação automática, formatação de erros).

  

5. **Evolução Facilitada**: Facilita trocar biblioteca HTTP no futuro sem afetar código que usa `ApiClient`.

  

#### 2.7.3 Problemas que Resolve

  

O padrão resolve os seguintes problemas:

  

1. **Interface Genérica Inadequada**: A biblioteca `http` retorna `Response` genérica, mas o projeto precisa de formato padronizado.

  

2. **Tratamento de Erros Inconsistente**: Sem adaptação, cada parte do código trataria erros HTTP de forma diferente.

  

3. **Lógica de Autenticação Espalhada**: Headers de autenticação precisariam ser adicionados manualmente em cada requisição.

  

4. **Duplicação de Código**: Lógica de parsing JSON, tratamento de erros e formatação seria repetida em múltiplos lugares.

  

5. **Dificuldade para Padronizar**: Sem centralização, seria difícil garantir formato consistente de requisições e respostas.

  

#### 2.7.4 Detalhes da Implementação

  

**Estrutura do Adapter:**

  

```dart

class ApiClient {

// Interface adaptada (específica do domínio)

static const String baseUrl = 'https://pinheiro-society-api.vercel.app';

// Adaptação da biblioteca http

static Future<Map<String, dynamic>> get(String endpoint) async {

try {

// 1. Preparar headers (adaptação)

final headers = await _getHeaders();

// 2. Chamar biblioteca http (interface original)

final res = await http.get(

Uri.parse('$baseUrl$endpoint'),

headers: headers,

);

// 3. Adaptar resposta para formato do domínio

return _adaptResponse(res);

} catch (e) {

// 4. Adaptar erros para formato do domínio

return {'success': false, 'error': 'Erro de conexão: ${e.toString()}'};

}

}

// Método privado para adaptar headers

static Future<Map<String, String>> _getHeaders() async {

final headers = Map<String, String>.from(_baseHeaders);

final token = await UserStorage.getToken();

if (token != null && token.isNotEmpty) {

headers['Authorization'] = 'Bearer $token';

}

return headers;

}

// Método privado para adaptar resposta

static Map<String, dynamic> _adaptResponse(http.Response res) {

// Verificar se é JSON

final contentType = res.headers['content-type'] ?? '';

if (!contentType.contains('application/json')) {

return {

'success': false,

'error': 'Resposta inválida do servidor',

};

}

// Parse JSON

dynamic data;

try {

data = jsonDecode(res.body);

} catch (e) {

return {

'success': false,

'error': 'Erro ao decodificar JSON',

};

}

// Adaptar para formato padronizado

if (res.statusCode == 200) {

return {'success': true, 'data': data};

}

return {

'success': false,

'error': data is Map

? (data['message'] ?? 'Erro na requisição')

: 'Erro na requisição',

};

}

}

```

  

**Características da Adaptação:**

  

1. **Interface Simplificada**:

- Original: `http.get(Uri, {headers})` retorna `Response`

- Adaptada: `ApiClient.get(String)` retorna `Map<String, dynamic>`

  

2. **Headers Automáticos**: Adiciona automaticamente:

- `Content-Type: application/json`

- `Accept: application/json`

- `Authorization: Bearer <token>` (quando disponível)

  

3. **Resposta Padronizada**: Sempre retorna:

  

```dart

{

'success': bool,

'data': dynamic, // quando success = true

'error': String // quando success = false

}

```

  

4. **Tratamento de Erros Centralizado**:

- Erros HTTP (404, 500, etc.)

- Erros de parsing JSON

- Erros de conexão

- Respostas não-JSON

  

5. **Validação de Conteúdo**: Verifica se resposta é JSON antes de tentar parsear

  

**Exemplo de Uso:**

  

```dart

// Interface adaptada (simples e específica do domínio)

final result = await ApiClient.get('/clientes');

  

// Não precisa conhecer detalhes de http, headers, parsing

if (result['success']) {

final clientes = result['data'];

// ... usar dados

} else {

final error = result['error'];

// ... tratar erro

}

```

  

**Comparação: Interface Original vs Adaptada**

  

**Sem Adapter (usando http diretamente):**

  

```dart

final response = await http.get(

Uri.parse('https://api.example.com/clientes'),

headers: {

'Content-Type': 'application/json',

'Authorization': 'Bearer $token',

},

);

  

if (response.statusCode == 200) {

final data = jsonDecode(response.body);

// ... usar dados

} else {

// ... tratar erro

}

```

  

**Com Adapter (usando ApiClient):**

  

```dart

final result = await ApiClient.get('/clientes');

if (result['success']) {

final data = result['data'];

// ... usar dados

} else {

final error = result['error'];

// ... tratar erro

}

```

  

**Vantagens da Adaptação:**

  

1. **Simplicidade**: Interface mais simples e intuitiva

2. **Consistência**: Formato padronizado em toda aplicação

3. **Manutenibilidade**: Lógica centralizada em um único local

4. **Evolução**: Fácil adicionar funcionalidades (cache, retry, logging)

5. **Testabilidade**: Fácil mockar para testes

  

**Métodos Adaptados:**

  

- `get(String endpoint)` - GET requests

- `post(String endpoint, Map body)` - POST requests

- `put(String endpoint, Map body)` - PUT requests

- `delete(String endpoint)` - DELETE requests

- `checkHealth()` - Health check sem autenticação

  

Todos seguem o mesmo padrão de adaptação: simplificam interface, adicionam funcionalidades e padronizam respostas.

  

---

  

## 3. Considerações Finais

  

### 3.1 Sinergia entre Padrões

  

Os padrões implementados no projeto Pinheiro Society trabalham em conjunto, criando uma arquitetura coesa e bem estruturada:

  

- **Repository + Adapter**: Repositórios usam `ApiClient` (Adapter) para comunicação HTTP, criando camada dupla de abstração

- **MVVM + Observer**: Controllers (ViewModels) usam Observer Pattern para notificar Views sobre mudanças

- **Factory + Models**: Factory Pattern cria Models a partir de dados da API, que são usados pelos Controllers

- **DI + Singleton**: Dependency Injection injeta controllers, enquanto Singleton fornece utilitários globais

- **Repository + MVVM**: Repositórios fornecem dados para Controllers, que gerenciam estado para Views

  

### 3.2 Benefícios da Arquitetura

  

A combinação desses padrões resulta em:

  

1. **Código Limpo e Organizado**: Separação clara de responsabilidades facilita compreensão

2. **Manutenibilidade**: Mudanças isoladas em uma camada não afetam outras

3. **Testabilidade**: Cada componente pode ser testado isoladamente

4. **Escalabilidade**: Fácil adicionar novas funcionalidades seguindo os padrões estabelecidos

5. **Reutilização**: Componentes podem ser reutilizados em diferentes contextos

  

### 3.3 Evolução Futura

  

A arquitetura atual facilita evoluções futuras:

  

- **Mudança de Backend**: Trocar API REST por GraphQL requer apenas adaptar repositórios

- **Novas Plataformas**: Adicionar suporte mobile reutiliza controllers e models

- **Testes Automatizados**: Estrutura facilita implementação de testes unitários e de integração

- **Performance**: Pode adicionar cache, lazy loading e outras otimizações sem quebrar arquitetura

  

### 3.4 Boas Práticas Seguidas

  

O projeto demonstra boas práticas de desenvolvimento:

  

- **SOLID Principles**: Especialmente Single Responsibility e Dependency Inversion

- **Clean Architecture**: Separação em camadas bem definidas

- **DRY (Don't Repeat Yourself)**: Lógica centralizada e reutilizada

- **Separation of Concerns**: Cada componente tem responsabilidade única

  

---

  

## 4. Referências

  

### 4.1 Documentação do Projeto

  

- **CONTEXTO_PROJETO.md**: Contexto completo do projeto Pinheiro Society

- **DOCUMENTO_APRESENTACAO.md**: Documentação técnica completa do sistema

  

### 4.2 Bibliotecas Utilizadas

  

- **Provider** (v6.1.2): [pub.dev/packages/provider](https://pub.dev/packages/provider)

- **http** (v1.1.0): [pub.dev/packages/http](https://pub.dev/packages/http)

- **Flutter ChangeNotifier**: [api.flutter.dev](https://api.flutter.dev/flutter/foundation/ChangeNotifier-class.html)

  

### 4.3 Padrões de Projeto

  

- **Design Patterns**: Gang of Four (GoF) - Padrões Clássicos de Projeto

- **MVVM Pattern**: [Microsoft MVVM Documentation](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/enterprise-application-patterns/mvvm)

- **Repository Pattern**: [Microsoft Repository Pattern](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design)

  

### 4.4 Arquitetura Flutter

  

- **Flutter Architecture Samples**: [flutter.dev/docs](https://flutter.dev/docs)

- **Provider Package Documentation**: [pub.dev/packages/provider](https://pub.dev/packages/provider)

  

---

  

**Documento gerado em**: Janeiro 2025

**Versão**: 2.0

**Projeto**: Pinheiro Society