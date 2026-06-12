Este módulo documenta o controle de prestação de serviços, processos de manufatura (transformação de insumos) e a gestão de ativos internos da empresa. O design do módulo prioriza a personalização profunda para atender a diferentes verticais de serviços (oficinas, assistências técnicas, indústrias, confecções).

---

## 1. Ordem de Serviço (OS) e Gestão de Equipamentos

A arquitetura da Ordem de Serviço permite modelar o cadastro de equipamentos de acordo com o nicho de mercado do cliente, evitando poluição visual com campos irrelevantes.

* **Campos Personalizáveis e Gatilhos de Busca:** O cadastro de equipamentos suporta até 20 campos inteiramente customizáveis.
    * *Cenário de Oficina Mecânica:* O administrador pode nomear o Campo 1 como "Veículo" e o Campo 2 como "Placa". O sistema possui uma inteligência nativa: ao digitar a placa no campo correspondente, ele busca automaticamente os dados do veículo associado.
    * O equipamento pode ser vinculado diretamente ao cliente, criando um histórico de manutenções daquele ativo. É possível definir o equipamento principal para que, ao abrir a OS, o sistema exiba apenas os campos essenciais.
* **Comissionamento Fracionado (Múltiplos Técnicos):** A OS permite a inserção de produtos (peças) e serviços (mão de obra). O sistema autoriza vincular **técnicos e vendedores diferentes para cada item da mesma OS**.
    * *Exemplo:* Em um conserto automotivo, a comissão da retífica do motor vai para o Técnico A, a manutenção elétrica para o Técnico B, e a comissão sobre a venda das peças vai para o Vendedor de Balcão C.
* **Situações (Status), Mensageria e Fotos:**
    * O administrador pode criar *status* customizados (ex: "Em Orçamento", "Aguardando Peça", "Em Execução") e aplicar cores para gestão visual na *grid*.
    * **Integração WhatsApp/E-mail:** Alterar o status da OS pode disparar uma notificação automática para o cliente informando o andamento do serviço.
    * **Galeria de Imagens:** Permite anexar fotos do equipamento no recebimento (comprovando avarias pré-existentes) e na entrega (qualidade do serviço).
* **Emissão de NFS-e:** O módulo está homologado com o Portal Nacional e a maioria dos provedores municipais para emissão nativa de Notas Fiscais de Serviço Eletrônicas.

---

## 2. Ordem de Produção (OP) e Lotes

O módulo de produção gerencia o ciclo de transformação, desde o empenho da matéria-prima (insumos) até a entrada do produto acabado no estoque.

* **Rotinas de Baixa e Apontamento:** A OP define em qual momento ocorrerá a movimentação de estoque. O sistema suporta cenários de **Produção Parcial** e apontamento de **Perdas na Produção** (quebras).
* **Rastreabilidade (Controle de Lote):**
    * O sistema pode gerar o lote do produto acabado automaticamente ou solicitar o preenchimento manual pelo operador.
    * Permite o rastreio cruzado: qual lote de insumo foi utilizado para fabricar determinado lote de produto final.
* **Gatilhos de Finalização:** O status da produção pode ser gerenciado de forma simplificada. O preenchimento da *Data de Produção* atua como um gatilho que finaliza automaticamente a OP e integraliza o saldo no estoque do produto acabado.
* **Bloqueios:** Assim como nas vendas, a produção possui travas que impedem a fabricação caso não haja estoque físico/contábil suficiente dos insumos necessários na ficha técnica.

---

## 3. Controle de Frota

Ferramenta de backoffice desenhada para o controle de ativos operacionais e veículos próprios da empresa.

* **Manutenção Preventiva e Corretiva:** Cadastro de manutenções vinculadas ao veículo interno (ex: troca de óleo, revisão de freios).
* **Controle de Odômetro:** Registro de quilometragem atual e previsão de quilometragem para a próxima manutenção.
* **Integração Financeira:** O registro de uma despesa com a frota permite a geração automática de um título no "Contas a Pagar", unificando o custo de manutenção ao fluxo de caixa principal da empresa.