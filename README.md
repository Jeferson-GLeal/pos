## 🖥️ POS (Point of Sale / PDV) Module

O módulo de **POS (PDV)** é a interface principal utilizada em operações de frente de loja, permitindo que operadores realizem vendas, controlem o caixa e consultem informações de catálogo em tempo real.  
Ele não funciona isoladamente: o POS atua como **orquestrador**, consumindo os microsserviços especializados para garantir que cada operação seja registrada, auditada e integrada ao restante do sistema.

### Microsserviços relacionados

1. **Cash Register Microservice**
   - Responsável pela abertura e fechamento de caixa.
   - Controla sangrias e suprimentos.
   - Fornece auditoria das movimentações por operador.
   - O POS consome esses endpoints para garantir que cada venda esteja vinculada a um caixa ativo.

2. **Sales Microservice**
   - Gerencia pedidos de venda, itens, pagamentos e orçamentos.
   - Permite emissão de notas fiscais ou recibos.
   - O POS utiliza esses endpoints para registrar cada transação de venda realizada no balcão.

3. **Catalog Microservice**
   - Centraliza informações de produtos e serviços (descrição, preço, estoque).
   - Permite adicionar, atualizar ou remover itens em pedidos.
   - O POS consulta o catálogo para exibir produtos disponíveis e validar preços durante a venda.

### Fluxo de Integração no POS
- **Operador abre o caixa** → POS chama o **Cash Register Microservice**.  
- **Cliente seleciona produtos** → POS consulta o **Catalog Microservice**.  
- **Venda é registrada** → POS envia dados ao **Sales Microservice**.  
- **Pagamento é processado** → POS atualiza o pedido e vincula ao caixa aberto.  
- **Auditoria e relatórios** → POS acessa endpoints de auditoria para rastrear movimentações por operador.  

### Benefícios da arquitetura
- **Modularidade**: cada microsserviço é independente e especializado.  
- **Escalabilidade**: permite evoluir ou substituir partes sem impactar o POS.  
- **Consistência**: garante que vendas, caixa e catálogo estejam sempre sincronizados.  
- **Auditabilidade**: todas as operações ficam registradas e rastreáveis por operador e período.  
