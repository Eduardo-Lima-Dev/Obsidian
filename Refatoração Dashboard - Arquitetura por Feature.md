## Estrutura de Pastas

```

lib/features/dashboard/

├── controllers/

│ ├── dashboard_controller.dart

│ ├── clientes_controller.dart

│ └── home_controller.dart

├── models/

│ ├── cliente.dart

│ ├── reserva.dart

│ ├── dashboard_summary.dart

│ └── estoque_alerta.dart

├── sections/

│ ├── home_section.dart

│ └── clientes_section.dart

├── widgets/

│ ├── stat_card.dart

│ ├── reservation_tile.dart

│ ├── stock_alert_tile.dart

│ ├── cliente_card.dart

│ ├── cliente_modal.dart

│ └── sidebar_item.dart

└── dashboard_screen.dart

```

## Etapa 1: Criar Models (lib/features/dashboard/models/)

### cliente.dart

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

### reserva.dart, dashboard_summary.dart, estoque_alerta.dart
Criar modelos similares para Reserva, DashboardSummary e EstoqueAlerta.
## Etapa 2: Criar Controllers (lib/features/dashboard/controllers/)
### dashboard_controller.dart
Responsável por gerenciar estado global do dashboard, navegação entre sections e auto-refresh.

```dart

class DashboardController extends ChangeNotifier {

String _selectedSection = 'inicio';

bool _isLoading = true;

String? _error;

Timer? _autoRefreshTimer;

  

String get selectedSection => _selectedSection;

bool get isLoading => _isLoading;

String? get error => _error;

  

void selectSection(String section) {

_selectedSection = section;

notifyListeners();

}

  

void startAutoRefresh(VoidCallback onRefresh) {

_autoRefreshTimer = Timer.periodic(

const Duration(seconds: 30),

(_) => onRefresh(),

);

}

  

@override

void dispose() {

_autoRefreshTimer?.cancel();

super.dispose();

}

}

```
### home_controller.dart
Gerencia dados da seção inicial (métricas, reservas, alertas).

```dart

class HomeController extends ChangeNotifier {

String reservasHoje = '-';

String totalClientes = '-';

String receitaHoje = '-';

String ocupacao = '-';

List<Reserva> proximasReservas = [];

List<EstoqueAlerta> alertasEstoque = [];

  

Future<void> carregarDados() async {

// Lógica atual de _carregarDados

}

}

```
### clientes_controller.dart
Gerencia CRUD de clientes, busca e modal.

```dart

class ClientesController extends ChangeNotifier {

final TextEditingController searchController = TextEditingController();

final TextEditingController nomeController = TextEditingController();

final TextEditingController emailController = TextEditingController();

final TextEditingController telefoneController = TextEditingController();

final TextEditingController cpfController = TextEditingController();

final GlobalKey<FormState> formKey = GlobalKey<FormState>();

final cpfMaskFormatter = MaskTextInputFormatter(...);

final telefoneMaskFormatter = MaskTextInputFormatter(...);

  

List<Cliente> clientes = [];

bool isSubmitting = false;

bool isEditing = false;

Cliente? clienteEditando;

Timer? searchDebounceTimer;

  

Future<void> carregarClientes() async { ... }

Future<void> salvarCliente() async { ... }

Future<void> deletarCliente(Cliente cliente) async { ... }

void buscarClientes() async { ... }

List<Cliente> getFilteredClientes() { ... }

@override

void dispose() {

searchController.dispose();

nomeController.dispose();

emailController.dispose();

telefoneController.dispose();

cpfController.dispose();

searchDebounceTimer?.cancel();

super.dispose();

}

}

```
## Etapa 3: Extrair Widgets (lib/features/dashboard/widgets/)
Mover widgets privados para arquivos separados:
- `_StatCard` → `stat_card.dart`
- `_ReservationTile` → `reservation_tile.dart`
- `_StockAlertTile` → `stock_alert_tile.dart`

- `_ClienteCard` → `cliente_card.dart`

- `_ClienteModal` → `cliente_modal.dart`

- `_SidebarItem` → `sidebar_item.dart`

  

Remover underscore e tornar públicos.

  

## Etapa 4: Criar Sections (lib/features/dashboard/sections/)

  

### home_section.dart

  

```dart

class HomeSection extends StatelessWidget {

final HomeController controller;

  

const HomeSection({required this.controller});

  

@override

Widget build(BuildContext context) {

return Column(

children: [

// Header com bem-vindo e logo

// Stat cards

// Painéis de reservas e alertas

],

);

}

}

```

  

### clientes_section.dart

  

```dart

class ClientesSection extends StatelessWidget {

final ClientesController controller;

  

const ClientesSection({required this.controller});

  

@override

Widget build(BuildContext context) {

return Column(

children: [

// Header

// Barra de busca e botão

// Lista de clientes

],

);

}

}

```

  

## Etapa 5: Refatorar DashboardScreen

  

Manter como StatefulWidget, mas delegar responsabilidades aos controllers:

  

```dart

class _DashboardScreenState extends State<DashboardScreen> {

late DashboardController _dashboardController;

late HomeController _homeController;

late ClientesController _clientesController;

  

@override

void initState() {

super.initState();

_dashboardController = DashboardController();

_homeController = HomeController();

_clientesController = ClientesController();

_homeController.carregarDados();

_dashboardController.startAutoRefresh(() {

if (_dashboardController.selectedSection == 'inicio') {

_homeController.carregarDados();

}

});

}

  

@override

Widget build(BuildContext context) {

return Scaffold(

body: Row(

children: [

// Sidebar

Expanded(

child: AnimatedBuilder(

animation: _dashboardController,

builder: (context, _) {

switch (_dashboardController.selectedSection) {

case 'inicio':

return AnimatedBuilder(

animation: _homeController,

builder: (context, _) => HomeSection(controller: _homeController),

);

case 'clientes':

return AnimatedBuilder(

animation: _clientesController,

builder: (context, _) => ClientesSection(controller: _clientesController),

);

default:

return Container();

}

},

),

),

],

),

);

}

  

@override

void dispose() {

_dashboardController.dispose();

_homeController.dispose();

_clientesController.dispose();

super.dispose();

}

}

```

  

## Etapa 6: Atualizar Imports

  

Atualizar `lib/main.dart` para importar de:

  

```dart

import 'features/dashboard/dashboard_screen.dart';

```

  

## Benefícios da Refatoração

  

1. **Separação de Responsabilidades**: Controllers focados, sections independentes

2. **Manutenibilidade**: Arquivos menores e mais focados (~200-400 linhas cada)

3. **Testabilidade**: Controllers podem ser testados isoladamente

4. **Reusabilidade**: Widgets podem ser reutilizados

5. **Escalabilidade**: Fácil adicionar novas sections/features

6. **Tipagem Forte**: Modelos tipados eliminam erros de runtime