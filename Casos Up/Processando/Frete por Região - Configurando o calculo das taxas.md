https://www.youtube.com/watch?v=g3zan5z8xZQ&pp=0gcJCT4LAYcqIYzv

Este módulo detalha o funcionamento e as diretrizes de parametrização da ferramenta de **Cálculo de Frete por Região/Bairro** no módulo de Delivery do ERP Código UP. O recurso foi desenvolvido para automatizar a cobrança de taxas de entrega com base na localização geográfica do cliente, reduzindo erros operacionais no momento da venda por telefone ou balcão `[00:00:00]`.

### 1. Hierarquia de Captura e Configuração da Taxa Padrão `[00:00:07]`

O motor de cálculo do ERP opera sob uma regra de contingência e fallback (retorno de segurança). O primeiro passo da parametrização exige que o administrador acesse as configurações globais do módulo de Delivery e defina um valor para a **Taxa de Entrega Padrão** (ex: R$ 4,00) `[00:00:07]`, `[00:01:09]`.

Essa taxa padrão funcionará como uma trava de segurança do sistema: se um operador registrar uma entrega para um bairro que não foi previamente mapeado em nenhuma região específica, o ERP não deixará a taxa zerada, injetando automaticamente o valor padrão configurado para proteger a margem da empresa `[00:00:15]`, `[00:02:59]`.

### 2. Estruturação do Cadastro de Regiões e Bairros `[00:00:23]`

No menu de _Cadastro de Regiões_, o gestor cria zonas logísticas customizadas e faz a amarração dos bairros correspondentes utilizando uma quebra de linha simples `[00:00:23]`:

- **Agrupamento em Lote (Input por Linha):** Para alimentar a região, o operador digita os nomes dos bairros um abaixo do outro na caixa de texto, pressionando a tecla `Enter` para separar cada localidade (ex: insere "Centro", pressiona `Enter`, insere "São Bernardo") `[00:03:38]`, `[00:00:47]`.
    
- **Diferenciação de Precificação:** O sistema permite associar valores de frete completamente distintos para cada grupo criado, como exemplificado no cenário de testes `[00:01:01]`:
    
    - **Região Central:** R$ 5,00 (Contendo bairros como Centro, São Bernardo, etc.) `[00:00:23]`, `[00:01:01]`.
        
    - **Região Dornelas:** R$ 17,00 (Contendo bairros como Dornelas, Santana, etc.) `[00:01:01]`.
        

### 3. Automação do Fluxo de Vendas e Detecção em Tempo Real `[00:01:11]`

Durante o atendimento operacional no Delivery, a identificação e a aplicação da taxa ocorrem de forma transparente e imediata na digitação do pedido `[00:01:11]`:

```
+-----------------------------------------------------------------------+
|                 FLUXO DE DETECÇÃO AUTOMÁTICA DE FRETE                 |
+-----------------------------------------------------------------------+
|                                                                       |
|  [Operador digita o Telefone/Endereço do Cliente]                     |
|                           │                                           |
|                           ▼                                           |
|  [ERP faz a varredura do Bairro informado]                            |
|                           │                                           |
|                           ┌───┴────────────────────────────────────┐  |
|                           ▼                                        ▼  |
|                 O Bairro está cadastrado?                     [ NÃO ] |
|                           │                                        │  |
|                        [ SIM ]                                     │  |
|                           │                                        ▼  |
|                           ▼                              Aplica a TAXA PADRÃO |
|              Identifica a Região Vinculada               (Ex: R$ 4,00)        |
|                           │                               [00:02:59]          |
|                           ▼                                           |
|              Aplica a TAXA DA REGIÃO                                  |
|         (Ex: Centro = R$ 5,00 | Dornelas = R$ 17,00)                  |
|               [00:01:26]  |  [00:02:20]                               |
+-----------------------------------------------------------------------+
```

- **Cenário A - Bairro Mapeado na Região Central `[00:01:19]`:** Ao localizar o cliente ou digitar o endereço associado ao bairro "Centro", o ERP detecta instantaneamente o vínculo com a _Região Central_ e injeta o valor de **R$ 5,00** no campo de taxa de entrega assim que a venda é iniciada `[00:01:19]`, `[00:01:26]`.
    
- **Cenário B - Bairro Mapeado na Região Dornelas `[00:02:06]`:** Ao lançar uma entrega para uma rua localizada no bairro "Dornelas", o motor do sistema altera o comportamento e fixa a taxa correspondente de **R$ 17,00** de forma automatizada `[00:02:06]`, `[00:02:31]`.
    
- **Cenário C - Bairro Não Cadastrado `[00:02:41]`:** Se o operador digitar um bairro que não foi catalogado no sistema (ex: "João XXIII") `[00:02:50]`, o ERP valida que nenhuma região foi atingida e aciona o fallback, cobrando o valor base de **R$ 4,00** parametrizado na configuração inicial `[00:02:59]`.