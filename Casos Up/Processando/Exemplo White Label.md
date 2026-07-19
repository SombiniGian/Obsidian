---
id:
  - CASO-148
link: https://www.youtube.com/watch?v=RTu4TUVlax4
setor:
  - Suporte
  - Implementação
modulo:
  - Periféricos / Impressoras Térmicas
tags:
  - epson
  - tm-t20x
  - impressora-termica
  - layout-grade
  - cupom
  - configuracao-windows
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Ajuste de Margem Epson]]
2. [[#Passo a Passo da Configuração no Windows]]
    1. [[#Acesso às Propriedades do Equipamento]]
    2. [[#Ajuste das Preferências de Impressão]]
    3. [[#Sincronização dos Padrões de Impressão (Spooler)]]
3. [[#Pontos Críticos e Regras de Negócio]]

# Visão Geral do Ajuste de Margem Epson
Durante a emissão de cupons não fiscais ou relatórios derivados do [[Configurações Globais / Interface Geral]] em impressoras térmicas não fiscais da marca Epson (especialmente o modelo TM-T20X), é comum ocorrer o sintoma de corte lateral de informações na área útil do papel. 

Este comportamento é causado pelo desalinhamento entre o tamanho de página enviado pelo gerador de relatórios do ERP e o driver nativo do Windows, que muitas vezes assume uma bobina de comprimento infinito, mas com margens físicas reduzidas. A correção definitiva exige a reconfiguração do tamanho de papel padrão diretamente nas propriedades avançadas do driver do spooler do Windows.

# Passo a Passo da Configuração no Windows

### Acesso às Propriedades do Equipamento
1. No sistema operacional Windows, abra o **Painel de Controle**.
2. Navegue até o caminho: **Hardware e Sons > Dispositivos e Impressoras**.
3. Localize o ícone correspondente ao hardware (ex: `EPSON TM-T20X Receipt`).
4. Clique com o botão direito sobre o ícone e selecione a opção **Propriedades da impressora**.

### Ajuste das Preferências de Impressão
Com a janela de propriedades aberta, o ajuste do papel deve ser feito na primeira camada de preferências:
1. Na aba **Geral**, clique no botão **Preferências...** localizado na base inferior.
2. Uma nova janela suspensa nomeada "Preferências de impressão" será exibida. Na aba **Layout**, clique no botão **Avançado...**.
3. Localize a variável estrutural **Tamanho do Papel**.
4. Altere a seleção que estiver marcada como padrão para a opção dimensional exata:
   * **Configuração Correta:** `Roll Paper 80 x 297 mm`
5. Clique em **OK** para fechar a janela avançada e depois em **OK** para aplicar as alterações nas Preferências.

### Sincronização dos Padrões de Impressão (Spooler)
Para garantir que o Windows aplique a regra para todos os usuários e sessões de caixa (evitando que o driver ignore a alteração após reiniciar o PC), a mesma configuração deve ser espelhada na aba de padrões avançados:

1. De volta à tela principal de "Propriedades da impressora", mude para a aba **Avançado**.
2. Clique no botão **Padrões de impressão...** localizado no canto inferior esquerdo.
3. Repita rigorosamente o processo anterior: clique em **Avançado...**, altere o **Tamanho do Papel** para `Roll Paper 80 x 297 mm`, clique em **OK** e feche as janelas secundárias.
4. Na janela principal de Propriedades, clique no botão **Aplicar** e depois em **OK** para selar a alteração no barramento do sistema operacional.

# Pontos Críticos e Regras de Negócio

> [!warning] Inversão de Layout de Páginas no PDV
> Definir o tamanho da bobina com dimensões erradas nas propriedades avançadas (como forçar folhas soltas A4 ou envelopes) fará com que o gerador de relatórios perca a referência do tamanho de corte da guilhotina automática. O [[PDV]] passará a saltar grandes áreas de papel em branco entre os cupons ou imprimirá caracteres distorcidos de forma horizontal, inviabilizando a operação da frente de caixa.

> [!tip] Teste de Alinhamento sem Consumo de Vendas
> Após concluir as alterações no driver do Windows, antes de reabrir o ERP ou executar vendas de teste, clique no botão **Imprimir Página de Teste** localizado na aba Geral das Propriedades da Impressora. Sendo o alinhamento de 80mm interpretado corretamente pelo hardware, o Windows imprimirá o sumário de drivers centralizado na bobina, sem cortes nas letras das extremidades esquerda e direita.