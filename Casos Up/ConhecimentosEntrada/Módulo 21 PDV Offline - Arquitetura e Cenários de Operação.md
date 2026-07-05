Este módulo detalha o funcionamento do PDV Offline, uma solução projetada para garantir a continuidade operacional em cenários de instabilidade de rede ou necessidades de descentralização, permitindo vendas autônomas que são sincronizadas posteriormente com o servidor na nuvem.

---

## 1. Conceito e Finalidade

O **PDV Offline** é um ponto de venda autônomo que opera com um banco de dados local. Sua principal função é resolver a dependência de conectividade constante com o servidor central, permitindo que a operação de venda continue mesmo sem acesso à internet ou à rede local.

* **Funcionalidades Suportadas:**
    * Realização de vendas (PDV).
    * Processamento de devoluções de venda.
    * Recebimento de contas a receber.
    * Cadastro de novos clientes.
* **O que não faz:** Operações de retaguarda como "Entrada de Nota Fiscal" devem ser realizadas na nuvem e, posteriormente, replicadas para o PDV offline através da sincronização de dados.

---

## 2. Infraestrutura e Topologia

O sistema permite diferentes arquiteturas dependendo da necessidade do cliente, seja para uma única empresa ou multiempresa.

### Cenário A: Multiempresa (Locais Distintos)

* Ideal para cadeias (ex: restaurantes) em que cada CNPJ está em um endereço físico diferente.
* Cada unidade possui seu servidor offline (banco de dados local).
* A nuvem atua como orquestrador e centralizador de dados.

### Cenário B: Supermercado (Alta Disponibilidade)

* Objetivo: Evitar a parada total em caso de falha na rede interna.
* Cada caixa atua como um "servidor" independente.
* Se o servidor central cair, os caixas individuais continuam vendendo. Se um computador estragar, os outros 9 permanecem operacionais.
* **Nota Técnica:** Cada estação configurada como PDV offline possui sua própria vida autônoma. Eles não conversam entre si, garantindo isolamento total de falhas.

---

## 3. Sincronização e Regras de Negócio

* **Sincronização Bidirecional:** Quando o link de rede é restabelecido, o PDV offline envia as vendas realizadas para o servidor na nuvem (ou local) automaticamente.
* **Limitação de Visibilidade:** Como o PDV offline trabalha de forma isolada, um caixa (PDV1) não enxerga as vendas feitas em outro caixa (PDV2) em tempo real. As informações só são consolidadas e visíveis globalmente quando replicadas para o servidor central.
* **Conectividade:** O PDV offline é indispensável em locais com infraestrutura de rede instável (ex: conexões Wi-Fi instáveis em mercearias/sorveterias), garantindo que a operação de vendas não seja interrompida.

---

## 4. Próximos Passos (Gatilhos e Personalizações)

O sistema oferece ferramentas avançadas de automação que estendem a capacidade do PDV Offline:

* **Gatilhos (Triggers/SQL):** Permitem executar comandos SQL baseados em eventos (ex: "ao incluir pedido"). Podem ser utilizados para validar grupos de produtos proibidos para venda a prazo, bloqueando automaticamente a operação se uma regra de negócio for violada.
* **Tela Personalizada:** O PDV moderno é altamente customizável. O administrador pode alterar a posição de elementos, cores, fontes e atalhos, adequando o software às necessidades específicas de produtividade do operador (ex: mapear teclas de atalho de sistemas anteriores para facilitar a transição).