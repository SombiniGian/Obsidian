Este módulo detalha as ferramentas de parametrização e o fluxo operacional do módulo de Ordem de Serviço (OS) do ERP, permitindo adaptar o sistema às regras de negócio específicas de cada segmento (oficinas, assistências técnicas, comércios) e automatizar o controle de manutenção.

1. Estrutura e Cadastros Base do Módulo de OS O funcionamento e a flexibilidade da Ordem de Serviço são sustentados por três pilares cadastrais, que moldam o comportamento do formulário e da interface de acordo com a atividade da empresa.
    

- **Tipos de Equipamentos (Campos Dinâmicos):** Permite configurar quais características e metadados serão exigidos no cadastro de cada item. Para o tipo "Veículo", por exemplo, o sistema habilita campos como placa, modelo e chassi; para "Celulares", campos como IMEI e operadora.
    
- **Vínculo com o Cliente:** Define se o equipamento possui um proprietário fixo associado de forma permanente (como um carro atrelado ao seu dono) ou se o item pode ser movimentado de forma independente na abertura da OS (como uma balança comercial).
    
- **Situações e Status Customizados:** Mapeamento do fluxo de trabalho interno da empresa (ex: _Aguardando, Em Manutenção, Aguardando Peça, Finalizado_). Permite definir a cor de exibição do registro na grade principal para facilitar a gestão visual.
    

2. Automações e Regras de Negócio (Painel Administrativo) A camada de parametrização avançada permite ao administrador injetar regras rígidas ou flexíveis na interface gráfica para acelerar o processo de abertura de ordens e garantir a integridade dos dados.
    

- **Gatilhos Automáticos de Status:** Configuração de transições automáticas no ciclo de vida da OS. O sistema permite definir qual status o registro assumirá imediatamente ao ser _Incluído_, _Faturado_, _Cancelado_ ou _Entregue_ (este último preenchendo automaticamente a data e hora de saída do equipamento).
    
- **Obrigatoriedade de Estruturas:** O administrador pode bloquear a digitação livre, obrigando o operador a selecionar um Equipamento e um Defeito previamente cadastrados no banco de dados.
    
    - _Caso de Uso:_ Essa restrição mitiga erros de digitação por parte do usuário (como variações de espaçamento ou ortografia) e garante a consistência do dataset para extração de relatórios estatísticos futuros.
        
- **Gerenciamento de Impressão Nativa (FastReport):** O sistema integra cada status a um layout de relatório específico. É possível parametrizar para que, ao mudar o status da OS para "Faturada", o motor do sistema dispare automaticamente a impressão do termo de garantia ou do recibo de entrega, sem necessidade de clique manual.
    

3. Fluxo Prático de Atendimento e Rateio de Comissões A interface operacional foi projetada para unificar o controle do laboratório técnico, o histórico de manutenção e o fechamento de caixa em uma estrutura integrada.
    

- **Designação e Filtros por Técnico:** No ato da abertura ou durante a movimentação da OS, o registro pode ser direcionado para um técnico ou laboratório específico. A interface do sistema permite segmentar a grade principal para exibir estritamente as ordens vinculadas ao usuário técnico que está logado na estação.
    
- **Lançamento Fracionado por Item (Peças e Serviços):** O técnico pode incluir múltiplos produtos e serviços dentro da mesma ordem de serviço. O sistema suporta o lançamento de um técnico/vendedor diferente para cada linha do documento.
    
- **Cálculo Automatizado de Comissões:** Com base nos lançamentos individuais por item, o motor financeiro processa o rateio e calcula as comissões devidas de forma separada para o vendedor das peças e para o técnico que realizou a mão de obra.
    
- **Trilha de Auditoria (Histórico da OS):** Um painel inferior na tela exibe de forma cronológica o histórico de movimentação do documento, registrando a data, a hora, as observações inseridas e quais usuários alteraram os status da OS.
    
- **Faturamento Integrado:** Ao concluir a manutenção, o encerramento da OS dispara o módulo financeiro padrão. O recebimento do valor (caixa/banco) gera a baixa automática, altera o status da OS para "Faturado" e emite o documento de saída do equipamento para o cliente final.
### 4. Faturamento Integrado e Emissão Fiscal (NFe)

O encerramento da Ordem de Serviço dispara o fluxo financeiro e fiscal do ERP, unificando a entrega do equipamento ao cumprimento das obrigações legais da empresa.

- **Validação de Garantia Nativa:** Ao faturar a OS, o sistema gera automaticamente o termo de garantia baseado nos produtos aplicados e serviços prestados, vinculando os prazos e condições ao cadastro do cliente e do equipamento.
    
- **Faturamento com Conversão Fiscal (NFe / NFSe):** O módulo permite a conversão direta dos itens da Ordem de Serviço em documentos fiscais de forma automatizada.
    
    - _Desdobramento de Itens:_ O motor fiscal do ERP separa o faturamento de mercadorias/peças substituídas (sujeitas ao ICMS via **NFe**) do faturamento da mão de obra/serviços técnicos (sujeitos ao ISSQN via **NFSe**).
        
    - _Sincronização de Regras de Negócio:_ Garante que a tributação, códigos fiscais (como CFOP e CST) e notas emitidas estejam perfeitamente amarrados à OS de origem, mitigando erros manuais de escrituração e agilizando a liberação do equipamento para o cliente final.
- ℹ️ **Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: https://www.youtube.com/watch?v=d-bBrW8SH9o e https://www.youtube.com/watch?v=LtdMeLDREgc