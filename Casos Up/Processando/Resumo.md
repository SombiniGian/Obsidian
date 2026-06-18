### 1. Autonomia e Customização White Label para Revendas `[00:00:09]`

O ERP foi integralmente projetado sob a ótica da descentralização técnica, permitindo que a revenda/distribuidor configure regras de negócio complexas sem a necessidade de acionar a equipe de programação principal `[00:00:16]`.

- **Identidade Visual Customizável (Rebranding):** A revenda pode alterar, por estação de trabalho, os seguintes elementos da interface gráfica para comercializar o software sob marca própria (White Label) `[00:06:06]`:
    
    - Logomarca da aplicação e imagem de fundo.
        
    - Título da aplicação e paleta de cores.
        
    - Supressão de referências à desenvolvedora original, permitindo o posicionamento do produto como tecnologia própria `[00:06:19]`.
        

### 2. Motor de Relatórios Parametrizável (Gerador FastReport) `[00:03:20]`

Todos os relatórios e documentos de impressão do ERP são customizáveis diretamente pela interface do sistema.

- **Edição Estilo Processador de Texto:** O gerador permite alterar fontes, tamanhos, cores e o posicionamento dos campos de forma visual (WYSIWYG), similar ao Microsoft Word `[00:04:23]`.
    
- **Acesso Nativo à Camada SQL `[00:04:30]`:** Usuários avançados ou técnicos da revenda possuem acesso direto às consultas SQL que alimentam os relatórios, permitindo otimizar queries, cruzar dados e injetar novos campos de banco de dados diretamente nos documentos `[00:04:35]`.
    
- **Múltiplos Modelos de Impressão Simultâneos `[00:03:41]`:** O sistema permite vincular mais de um layout a uma mesma tela (ex: emitir um comprovante em formato 80 colunas para bobina térmica ou em formato A4 para impressoras convencionais) `[00:03:56]`.
    
- **Painel Compartilhado de Relatórios `[00:04:08]`:** A revenda possui acesso a um repositório central contendo layouts desenvolvidos por outros canais, acelerando a implantação de novos modelos nos clientes finais `[00:04:13]`.
    

### 3. Rastreabilidade Avançada e Trilha de Auditoria `[00:07:22]`

O ERP conta com um mecanismo de segurança de dados (log) que grava as transações diretamente na camada de persistência.

- **Auditoria de Célula:** Toda modificação em qualquer formulário registra o histórico exato da alteração, contendo:
    
    - Usuário responsável e timestamp (data/hora).
        
    - O campo exato que sofreu a modificação.
        
    - O valor original (antigo) e o novo valor gravado (ex: alteração de preço de venda ou mudança de grupo tributário) `[00:07:36]`.
        

### 4. Engenharia de Estoque e Recursos Específicos por Nicho `[00:06:36]`

Além do cadastro unificado de entidades e da conversão automatizada de unidades de medida `[00:06:38]`, o núcleo do estoque possui tratamentos específicos para mercados verticais:

- **Rastreabilidade por Lote e Validade `[00:07:10]`:** Controle obrigatório de lotes tanto na entrada por XML de compra quanto na saída (faturamento). Permite o atendimento a exigências regulatórias de mercados como farmácias/medicamentos (controle de validade) e comércio de dispositivos móveis (número de série/IMEI) `[00:07:16]`.
    
- **Módulo de Logística Reversa de Vasilhames `[00:08:07]`:** Controle automatizado de comodatos e vasilhames vazios (ex: distribuidoras de gás, oxigênio medicinal e bebidas). No momento da venda do produto cheio, o sistema executa a baixa do item e, em paralelo, abre um saldo devedor ou gera a entrada automatizada do casco vazio no estoque logístico `[00:08:13]`.
    
- **Módulo Restaurante (Complementos e Preparo) `[00:08:38]`:** O cadastro de produtos suporta a injeção de complementos e modificadores de modo de preparo vinculados ao módulo de controle de mesas e comandas eletrônicas `[00:08:46]`.
    
- **Gestão de Recorrência (Mensalidades/Clube) `[00:09:18]`:** Motor de cobrança integrado para o gerenciamento de contratos mensais, semestrais ou anuais, voltado para prestadores de serviço, clubes, academias e o próprio controle de carteira de clientes da revenda `[00:09:26]`.
ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: https://www.youtube.com/watch?v=WZ2pAc1Mxb0&pp=0gcJCT4LAYcqIYzv