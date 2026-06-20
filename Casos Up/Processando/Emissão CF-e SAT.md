# Emissão de CF-e SAT (Modelo 59)

## 1. Resumo Executivo

Este guia descreve os protocolos de implementação e a rotina operacional para a emissão de Cupom Fiscal Eletrônico (CF-e) via hardware SAT no ERP Código UP. O processo diferencia-se das demais modalidades fiscais pela descentralização da numeração e alta performance de autorização via hardware.

## 2. Configurações de Ambiente

### 2.1. Natureza de Operação

Define a regra fiscal que o sistema aplicará à transação.

- **Caminho:** `Cadastros` > `Natureza de Operação`
    
- **Campos Críticos:**
    
    - **Modelo:** Selecionar obrigatoriamente `59` (CF-e SAT).
        
    - **Controle de Numeração:** Não aplicável (o número é gerado pelo hardware SAT).
        

### 2.2. Configuração do Hardware SAT

Parametrização da comunicação entre o ERP e o equipamento.

- **Caminho:** `Documentos Fiscais` > `Configuração SAT`
    
- **Campos Críticos:**
    
    - **Tipo de Comunicação:** `Local` (DLL na mesma máquina) ou `Servidor` (via IP/Porta).
        
    - **DLL de Comunicação:** Caminho do diretório contendo a `.dll` específica fornecida pelo fabricante do equipamento.
        
    - **Código de Ativação:** Definido no momento da inicialização do hardware.
        
    - **Servidor SAT:** Caso o equipamento esteja em rede, configurar IP e Porta no executável de background (_Servidor SAT_).
        

## 3. Fluxo Operacional (PDV)

### 3.1. Emissão de Cupom

O processo de venda é otimizado para o modelo balcão.

- **Caminho:** `Pedido de Venda` (Tipo: Balcão)
    
- **Fluxo de Ação:**
    
    1. Inserção de itens (código/leitura de barras).
        
    2. Seleção de forma de pagamento vinculada ao PDV.
        
    3. Finalização via comando de transmissão (processamento em milissegundos).
        
    4. Impressão automática via _Gerador de Relatórios_ ou via porta direta (configurável).
        

### 3.2. Cancelamento de Cupom

Protocolo para anulação de documentos fiscais já autorizados.

- **Caminho:** `Histórico de Vendas` > `Selecionar Cupom` > `Botão Cancelar`
    
- **Campos Críticos:**
    
    - **Justificativa:** Preenchimento obrigatório para auditoria fiscal interna.
        
    - **Confirmação:** O ERP envia comando de exclusão direta ao hardware SAT para registro do cancelamento.
        

## 4. Arquitetura de Comunicação e Segurança

- **Monitoramento:** Utilize o "Servidor SAT" (minimizado na bandeja do Windows) para verificar logs operacionais, status de conexão e erros de comunicação (`IP`, `Porta`, `Status: Online/Offline`).
    
- **Assinatura:** A vinculação do CNPJ da _Software House_ e da empresa emitente ao hardware SAT deve ser realizada obrigatoriamente via portal Sefaz-SP antes do primeiro uso.
    
- **Auditoria:** Toda alteração de parâmetros ou cancelamento é registrada nos logs do sistema para garantir conformidade perante órgãos fiscalizadores.
    

## 5. Conclusão e Suporte

Esta estrutura garante alta disponibilidade na emissão de cupons fiscais, reduzindo a dependência de chamadas constantes aos servidores do Sefaz. Em caso de falhas de comunicação, verifique primeiro o status do "Servidor SAT" e o mapeamento da DLL.

**Consulte o vídeo tutorial para detalhes adicionais de visualização:** [Assista ao vídeo: Emissão CF-e SAT](https://www.youtube.com/watch?v=elcnR9FsFyY&t=53s)