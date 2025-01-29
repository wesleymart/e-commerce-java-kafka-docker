


Esse projeto tem como objetivo ser:

    • Totalmente desacoplado → Microserviços podem evoluir independentemente.
    • Resiliência → Se um serviço falhar, os eventos são processados assim que voltar ao ar.
    • Escalabilidade → Kafka permite paralelismo para processar milhões de pedidos simultaneamente.
    • Alta Disponibilidade → Pode rodar em Kubernetes para escalar automaticamente.

E para isso vai usar as seguintes tecnologias no seu desenvolvimento:

Java 17 - Linguagem principal
Spring Boot 3 - Framework para microsserviços
Spring Cloud - Comunicação entre microserviços
Apache Kafka - Processamento de eventos
MongoDB - Banco de dados para persistência
Redis - Cache para melhorar desempenho
Docker - Implantação e orquestração
JWT + OAuth2 - Autenticação e segurança


Principais funcionabilidades:

Cadastro e Gerenciamento de Produtos
    • Microserviço de Catálogo para listar e gerenciar produtos.
    • Integração com um banco de dados NoSQL (MongoDB ou Elasticsearch) para buscas rápidas.
Carrinho de Compras e Checkout
    • Microserviço para adicionar e remover itens do carrinho.
    • Comunicação síncrona com o serviço de autenticação para validar o usuário.
Processamento de Pedidos (Order Service)
    • Ao finalizar a compra, um evento "OrderCreated" é enviado para o Kafka.
    • Diferentes microserviços consomem esse evento para iniciar os próximos passos.
Pagamentos com Gateway (Payment Service)
    • O serviço de pagamento escuta o evento "OrderCreated" e tenta processar o pagamento.
    • Em caso de sucesso, emite um novo evento "PaymentApproved", caso contrário, "PaymentFailed".
Envio de Notificações
    • O serviço de Notificações escuta eventos para enviar e-mails e mensagens de confirmação via Kafka + WebSockets.
Entrega e Rastreamento (Shipping Service)
    • Se o pagamento for bem-sucedido, o serviço de envio recebe o evento "PaymentApproved" e inicia a logística.

