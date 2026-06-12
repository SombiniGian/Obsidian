Este módulo detalha a configuração prática das estações de trabalho em ambiente PDV Offline, abordando a independência operacional, estratégias de contingência e o funcionamento da lógica de replicação de dados.

---

## 1. Configuração de Estações de Trabalho

A instalação do PDV Offline é segmentada em duas funções distintas dentro da rede local:

* **Servidor Local (PDV Offline):** A estação que recebe a instalação do banco de dados local. Esta máquina torna-se o núcleo de processamento do PDV para aquela unidade física.
* **Estações (Terminais):** Máquinas adicionais utilizadas para realizar as vendas. Elas não possuem banco de dados próprio, sendo configuradas para apontar diretamente para o *Servidor Local*.
* **Segregação de Cargas:** O sistema permite definir qual computador será responsável por processar a carga de dados. Essa configuração deve ser centralizada para evitar conflitos de atualização e garantir que o *Servidor Local* mantenha o *dataset* sempre atualizado a partir da nuvem.

## 2. Independência e Autonomia

O principal valor desta arquitetura é a capacidade de sobrevivência do ponto de venda.

* **Vida Autônoma:** Uma vez configurado como PDV Offline, o terminal possui uma base de dados completa (produtos, preços, clientes). 
* **Resiliência a Falhas:** Caso ocorra a queda da rede (corte do cabo de rede ou falha na infraestrutura de internet), o sistema não interrompe a operação. O PDV continua permitindo vendas, devoluções e recebimentos normalmente, pois consulta exclusivamente o banco local.
* **Isolamento de Erros:** Em cenários como supermercados com múltiplos caixas, a falha de uma estação (ou a interrupção do servidor central) não paralisa as demais. Cada PDV Offline preserva sua autonomia, evitando o efeito cascata de parada de operação.

## 3. Lógica de Replicação de Dados

A sincronização entre o PDV Offline e a retaguarda na nuvem é gerenciada pelo motor de replicação:

* **Upload em Background:** As transações realizadas em modo offline são armazenadas localmente. Assim que a conectividade com a nuvem é detectada, o sistema inicia automaticamente a replicação dos dados pendentes para o servidor central.
* **Limitação de Escopo:** É vital compreender que a replicação é um processo assíncrono. Vendas realizadas em um terminal offline não são visíveis em outros terminais ou na nuvem em tempo real até que a sincronização seja concluída.
* **Priorização:** O sistema é otimizado para que a operação de venda (frente de caixa) tenha prioridade máxima, relegando as tarefas de sincronização para momentos em que o processamento do PDV não seja afetado.