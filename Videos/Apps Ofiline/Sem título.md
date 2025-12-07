graph TD
    subgraph "Celular do Usuário A (Offline)"
        A1[Abre Cadastro do Cliente] --> A2[Ação: EDITA o endereço];
        A2 --> A3[Salva 'Edição' no BD Local A];
    end

    subgraph "Celular do Usuário B (Offline)"
        B1[Abre Cadastro do mesmo Cliente] --> B2[Ação: APAGA o cadastro];
        B2 --> B3[Salva 'Exclusão' no BD Local B];
    end

    A3 -.-> C{Ambos recuperam<br/>Conexão};
    B3 -.-> C;
    C --> D[Servidor recebe as duas ações pendentes];
    D --> E{{CONFLITO!}};
    E --> F[O que fazer? Editar ou Apagar?];
    style E fill:#ffcccb,stroke:red,stroke-width:2px

