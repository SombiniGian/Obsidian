
---
id: [CASO-012]
link: https://www.youtube.com/watch?v=pQvqPpjv4sI
setor: [Suporte, Implementação, Operacional]
modulo: [Mobile / Força de Vendas]
tags: [android, força-de-vendas, aplicativo, vpn, configuração-remota, sincronização]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Aplicativo]]
2. [[#Arquitetura de Configuração Centralizada]]
3. [[#Primeiro Acesso e Ativação no Dispositivo]]
4. [[#Sincronização de Dados e Carga Inicial]]
5. [[#Operação e Lançamento de Pedidos]]
6. [[#Pontos Críticos e Regras de Segurança]]

# Visão Geral do Aplicativo
O aplicativo **Android Força de Vendas UP** é uma ferramenta móvel desenvolvida para equipes de vendas externas. Ele opera de forma híbrida (Offline/Online), permitindo que o vendedor consulte o catálogo de produtos, verifique dados cadastrais de clientes, aplique tabelas de preços e registre pedidos mesmo sem conectividade com a internet. O tráfego de dados com o servidor de retaguarda ocorre apenas nos momentos de sincronização de carga e no envio de novos pedidos. O sistema conta ainda com suporte nativo a múltiplos CNPJs (Multi-Empresa).

# Arquitetura de Configuração Centralizada
Para eliminar a necessidade de configurar manualmente parâmetros complexos de rede — como endereços IP públicos, chaves de DNS Dinâmico ou portas de comunicação — em cada dispositivo móvel da equipe, o sistema utiliza um modelo de provisionamento remoto via painel administrativo.

### Parametrização na Retaguarda (Painel Web)
O administrador do sistema realiza a configuração global acessando o cadastro de força de vendas na retaguarda. Os seguintes campos devem ser preenchidos:
*   **IP / DNS:** O endereço de rede do servidor de banco de dados ou da API (pode ser o IP real, DNS ou o IP gerado através de uma rede virtual [[Redes e Conectividade Externa]]).
*   **Porta:** A porta lógica configurada para escuta no servidor de comunicação.
*   **Cor Exclusiva:** Definição da identidade visual do aplicativo (ex: Laranja, Azul). O layout do app se adapta à cor selecionada após a sincronização.
*   **Logomarca:** Upload da imagem da empresa ou da revenda que será exibida na tela de abertura do aplicativo.
*   **Token / Senha de Ativação:** Chave de segurança de formato livre (ex: `123`) gerada no painel que valida o pareamento do dispositivo.

# Primeiro Acesso e Ativação no Dispositivo
Ao instalar o aplicativo pela primeira vez no dispositivo Android, o sistema exibirá uma tela de autenticação de infraestrutura simplificada.

```json
{
  "ativacao_dispositivo_mobile": {
    "cnpj_empresa": "00000000000000",
    "senha_ativacao": "123",
    "comportamento_esperado": "O aplicativo consome a API da UP Sistemas, localiza o IP/Porta e a identidade visual parametrizados para o CNPJ e aplica as configurações localmente."
  }
}
````

### Passos para Ativação:

1. Abra o aplicativo no smartphone.
    
2. Insira o **CNPJ** da empresa detentora da licença.
    
3. Insira a **Senha de Ativação** configurada no painel de retaguarda.
    
4. Clique em **Baixar Configurações**.
    
5. O aplicativo mudará automaticamente de cor e exibirá a logomarca da empresa.
    
6. Clique em **Salvar** para fixar os parâmetros de comunicação no armazenamento local do aparelho.
    

# Sincronização de Dados e Carga Inicial

Com o canal de comunicação estabelecido, o vendedor precisa baixar o pacote de dados comerciais para conseguir trabalhar em modo offline.

### Mecânica de Sincronização:

- No menu superior direito, clique em **Atualizar Dados**.
    
- **Otimização de Payload (Tráfego de Imagens):** Por padrão, as caixas de seleção para download de imagens de clientes e fotos de produtos vêm desmarcadas. Devido ao grande volume e peso dos arquivos binários, realizar o download das mídias em redes móveis (3G/4G) pode causar lentidão ou falhas por _Timeout_. Caso as fotos sejam cruciais, marque as opções manualmente antes de iniciar a carga.
    
- Após o processamento, as tabelas de **Clientes**, **Produtos** (com códigos de barras, unidades de medida e conversões) e **Empresas** ficam salvas no banco local SQLite do smartphone.
    

# Operação e Lançamento de Pedidos

O fluxo de digitação de propostas foi estruturado para mitigar erros de preenchimento, sinalizando campos obrigatórios e automatizando heranças de cadastros.

### Criação do Pedido:

1. Acesse o módulo de pedidos e selecione a **Empresa** (contexto multi-empresa).
    
2. Os campos com validação obrigatória são destacados na cor **vermelha** na interface.
    
3. Selecione o **Cliente**. Ao carregar a pessoa, o aplicativo herda de forma automática a **Tabela de Preço** e a **Forma de Pago** vinculadas a ela no ERP.
    
4. Defina a **Data Provável de Entrega**.
    

### Adição de Itens ao Carrinho:

- **Via Toque/Deslize:** Na listagem de produtos, arraste o item para o lado para definir a quantidade padrão ou clique sobre ele para digitar os valores em uma janela auxiliar.
    
- **Via Código de Barras:** Clique no botão de câmera localizado no **canto inferior direito** da tela. O aplicativo acionará a câmera traseira do smartphone como um leitor óptico de alta velocidade. Ao ler o código de barras válido, o item é adicionado ao carrinho, restando ao vendedor informar apenas a quantidade.
    

### Transmissão dos Documentos

Após salvar o pedido, ele ficará com o status de `Em Aberto` localmente.

- O operador pode filtrar os registros clicando na guia de **Não Enviados**.
    
- Para enviar os dados à central da empresa, clique no botão de menu e selecione a opção **Enviar**.
    
- Uma vez processado pela API, o status muda para `Enviado` e o documento fica disponível na tela de faturamento de pedidos do ERP na retaguarda.
    

# Pontos Críticos e Regras de Segurança

> [!warning] Validação de Bloqueio por Falha de Sincronização
> 
> Caso o vendedor altere preços, prazos ou condições comerciais de um cliente na retaguarda e não execute a rotina de **Atualizar Dados** no aplicativo, o dispositivo móvel continuará aplicando as regras antigas gravadas no banco local, gerando divergências financeiras no momento em que o pedido for transmitido e confrontado pelo servidor de retaguarda.

> [!danger] Timeout em Carga de Imagens Completa
> 
> Forçar a sincronização de dados contendo milhares de imagens de produtos utilizando redes móveis instáveis resultará em quebras de conexão e corrupção da base local. Recomenda-se realizar a primeira carga de imagens obrigatoriamente conectados a uma rede Wi-Fi estável.

