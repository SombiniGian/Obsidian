Este módulo detalha os processos de infraestrutura, as regras de negócio para lançamento, o ciclo de vida dos documentos e o fluxo de arquivos eletrônicos (Remessa e Retorno) para a gestão de **Boletos Bancários** no ERP Código UP.

### 1. Arquitetura de Configuração e Cadastro Estrutural `[00:00:01]`

Para habilitar a emissão de cobranças bancárias, o sistema exige a parametrização de duas tabelas fundamentais que servem de base para o motor financeiro:

- **Tabela de Tipos de Documento `[00:00:09]`:** Deve existir um registro específico configurado com a flag de movimentação de boletos bancários ativa `[00:00:17]`. O ERP oferece flexibilidade na organização:
    
    - _Modelo Granular:_ Cadastro de múltiplos tipos de documentos isolados por bandeira/banco (ex: "Boleto Sicoob", "Boleto Bradesco") `[00:00:27]`.
        
    - _Modelo Unificado:_ Cadastro de um único tipo genérico (ex: "Boleto Bancário") que é dinamicamente vinculado a qualquer conta corrente no ato da emissão `[00:03:53]`.
        
- **Tabela de Contas Correntes / Agências `[00:00:34]`:** No cadastro da conta bancária, uma aba dedicada à emissão de boletos armazena as chaves de integração bancária `[00:01:04]`:
    
    - _Metadados Bancários:_ Número da conta, agência, código do banco, titularidade, número do convênio, código da carteira e layout padrão (CNAB 240 ou CNAB 400) `[00:01:04]`.
        
    - _Diretórios do Sistema FileSystem:_ Caminhos de rede locais destinados à exportação dos arquivos de remessa (`.rem`) e importação dos arquivos de retorno (`.ret`) `[00:01:25]`.
        
    - _Regras de Cobrança:_ Instruções de local de pagamento, mensagens fixas de instrução no DANFE/boleto, parâmetros de dias para protesto automático, taxas de juros de mora e multas por atraso `[00:01:31]`.
        

### 2. Lançamento Avulso e Acoplamento Lógico com Recebimentos `[00:02:15]`

O ERP trata o boleto físico de forma desacoplada da provisão financeira, gerando uma amarração de dependência para garantir a consistência das contas.

- **Filtro de Tipos de Documento no Lançamento:** Ao lançar um Contas a Receber (Recebimento) manual, o sistema filtra e exibe no campo "Tipo de Documento" estritamente as modalidades configuradas para operações a prazo (ex: Duplicata, Crédito) `[00:03:01]`.
    
- **Geração da Cobrança em Lote ou Unitária `[00:03:36]`:** Na grade de Recebimentos, o operador pode selecionar um ou mais títulos em aberto e acionar o comando **"Gerar Boleto"** `[00:03:46]`. O sistema exibe as contas bancárias ativas e, após a confirmação, o ERP processa a codificação da linha digitável e atualiza o status do título financeiro de "Débito Normal" para "Boleto Bancário" `[00:04:11]`.
    
- **Bloqueio de Edição Estrita por Vínculo `[00:04:34]`:** Assim que um título financeiro é acoplado a um boleto, o sistema **bloqueia qualquer tentativa de alteração manual direta** nos dados desse recebimento (como valor ou vencimento) `[00:04:34]`. Essa trava impede discrepâncias entre o que foi impresso para o cliente e o que está registrado no banco de dados Firebird `[00:04:42]`.
    
- **Ciclo de Recorrência (Substituição de Cobrança) `[00:04:59]`:** Caso seja necessário alterar a data de vencimento ou os valores de um título já emitido, o operador deve obrigatoriamente **cancelar o boleto ativo** `[00:04:59]`. O cancelamento desvincula o título, que retorna ao status de "Débito Normal", permitindo a edição e a emissão de um novo boleto para a mesma conta ou para um banco concorrente `[00:05:08]`.
    

### 3. Ciclo de Vida e Estados do Boleto Bancário `[00:01:50]`

No painel de _Movimentações de Boletos Bancários_, os documentos transitam por uma esteira de estados controlada por regras de negócios automáticas `[00:01:50]`:

- **Em Aberto:** Boleto gerado e impresso no sistema, porém ainda não comunicado à instituição financeira (pendente de envio na remessa) `[00:01:59]`.
    
- **Enviado ao Banco:** Boleto exportado em um lote de remessa e transmitido ao banco `[00:01:59]`.
    
- **Baixado / Liquidado:** Ocorrência que confirma o pagamento do boleto pelo cliente final via compensação bancária `[00:02:06]`.
    
- **Descontado:** Estado ativado quando a empresa realiza a operação de antecipação de recebíveis (desconto de duplicatas) junto ao banco, recebendo o crédito antecipado `[00:02:06]`.
    
- **Cancelado:** Documento invalidado administrativamente pelo operador `[00:02:15]`.
    

### 4. Engenharia de Arquivos Eletrônicos: Fluxo de Remessa `[00:05:39]`

O processo de comunicação oficial das carteiras registradas segue um fluxo homologado de geração e validação de lotes CNAB.

```
+------------------+         1. Comando Gerar          +-------------------+
| Boletos Gerados  | --------------------------------> | Seleção de Banco  |
|  (Status: Aberto)|                                   | (Sicoob / BB / ..)|
+------------------+                                   +-------------------+
                                                                 |
                                                                 | 2. Filtro Automático
                                                                 v
+------------------+         4. Exportação             +-------------------+
| Arquivo REMESSA  | <-------------------------------- | Grade de Boletos  |
|  (Pasta Local)   |                                   |   Filtrados       |
+------------------+                                   +-------------------+
        |
        | 5. Upload p/ Banco
        v
+------------------+         6. Confirmação de Envio   +-------------------+
| Validação Banco  | --------------------------------> | Status Atualizado |
|  (Registro)      |                                   |   (Enviado)       |
+------------------+                                   +-------------------+
```

- **Agrupamento e Filtro por Carteira `[00:05:39]`:** Ao acessar a rotina de remessa, o operador seleciona a conta corrente de destino (ex: Sicoob) `[00:05:50]`. O sistema limpa a grade e exibe **apenas os boletos gerados para aquela instituição específica** `[00:05:55]`.
    
- **Geração do Arquivo Física `[00:06:07]`:** O comando de geração compila as linhas selecionadas no layout CNAB configurado e exporta o arquivo estruturado diretamente na pasta física mapeada no cadastro da empresa `[00:06:07]`.
    
- **Painel de Controle e Rastreabilidade de Lotes `[00:06:16]`:** Uma aba de histórico exibe todas as remessas geradas no sistema `[00:06:16]`. O ERP oferece uma trava de segurança baseada no status do envio:
    
    - _Antes da Transmissão:_ Se o operador perceber um erro na geração (ex: ausência de CPF do sacado), ele pode acionar a opção **"Cancelar Remessa"** `[00:06:24]`. O lote é descartado e todos os boletos contidos nele retornam imediatamente para o status "Aberto", ficando disponíveis para correção e nova exportação `[00:06:30]`.
        
    - _Após a Transmissão:_ Uma vez que o operador realiza o upload do arquivo no internet banking, ele executa o comando **"Confirmar Envio"** no ERP `[00:06:49]`. O sistema altera definitivamente o status dos boletos para **"Enviados"** e **bloqueia irreversivelmente a exclusão ou cancelamento do lote de remessa**, garantindo a integridade do histórico contábil `[00:06:55]`.
        

### 5. Regras de Custos de Cancelamento Pós-Remessa `[00:07:18]`

O momento em que um boleto é cancelado determina o fluxo tributário e de custos operacionais com a instituição bancária:

- **Cancelamento Pré-Remessa:** Se o documento for cancelado enquanto estiver no status "Aberto" (antes de figurar em qualquer arquivo de remessa), o ERP simplesmente invalida o registro localmente. Como o banco nunca tomou conhecimento do título, **não há geração de tarifas de registro ou cancelamento** `[00:07:44]`.
    
- **Cancelamento Pós-Remessa:** Se o boleto for cancelado após a confirmação de envio da remessa, o ERP altera o status do boleto e injeta automaticamente essa linha de cancelamento no próximo arquivo de remessa a ser gerado `[00:07:25]`. Isso é obrigatório para instruir o banco a dar baixa na cobrança registrada em sua base de dados, o que **sujeita a operação às tarifas de manutenção e baixa do contrato bancário** `[00:08:00]`.
- 
**Nota de Apoio:** Se restarem dúvidas ou se necessitar de assistência visual durante a leitura deste guia operacional, poderá assistir ao vídeo demonstrativo passo a passo diretamente no YouTube através do seguinte link: https://www.youtube.com/watch?v=8j3AqG6P2Hg&pp=0gcJCT4LAYcqIYzv