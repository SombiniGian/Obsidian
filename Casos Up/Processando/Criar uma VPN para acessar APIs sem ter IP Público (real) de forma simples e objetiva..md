
---
id: [CASO-004]
link: https://www.youtube.com/watch?v=OmAoied-4-8
setor: [Suporte, Infraestrutura, Implementação]
modulo: [Redes e Conectividade Externa]
tags: [vpn, zerotier, conexao-externa, api, forca-de-vendas, relatorio-zap]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral da Solução]]
2. [[#Criação e Configuração da Rede Virtual (ZeroTier)]]
3. [[#Instalação e Vínculo do Cliente no Servidor (Windows)]]
4. [[#Conexão e Homologação de Dispositivos Móveis (Android/iOS)]]
5. [[#Validação de Acesso às APIs e Serviços]]
6. [[#Pontos Críticos e Regras de Segurança]]

# Visão Geral da Solução
Esta documentação aborda a criação e a parametrização de uma Rede Privada Virtual (VPN) utilizando a plataforma ZeroTier. A solução é indicada para cenários onde parceiros e revendas enfrentam dificuldades técnicas para expor as APIs do sistema para a internet (ex: [[Servidor Força de Vendas]], [[Relatório Zap]], consultas externas de banco de dados). 

A arquitetura elimina a necessidade de infraestrutura complexa, tais como:
*   Contratação de IP Público Fixo junto a provedores de internet.
*   Configurações de redirecionamento de portas (*Port Forwarding*) em modems e roteadores.
*   Parametrização e manutenção de serviços de DNS Dinâmico (DDNS/No-IP).

O ZeroTier encapsula o tráfego simulando que todos os dispositivos conectados (Servidores, Computadores e Smartphones) façam parte de uma mesma rede local (LAN), independentemente de sua localização geográfica ou tipo de conexão à internet (Wi-Fi, 4G, 5G).

# Criação e Configuração da Rede Virtual (ZeroTier)

### 1. Registro e Acesso à Plataforma
1. Acesse o portal oficial em `zerotier.com`.
2. Realize o cadastro ou efetue o login (suporta autenticação rápida via conta Google).
3. Na interface administrativa principal, clique no botão **Create a Network**. O sistema gerará uma nova rede contendo um identificador exclusivo de 16 caracteres (**Network ID**).

### 2. Parametrização Interna da Rede
Clique sobre a rede recém-criada para acessar o painel de configurações e ajuste os seguintes blocos:

*   **Basics:** No campo **Network Name**, atribua um nome descritivo para facilitar o gerenciamento (ex: `VPN Vendas`).
*   **Access Control:** Defina o nível de segurança de ingresso na rede:
    *   **Private (Privado - Recomendado):** Exige que o administrador do painel aprove manualmente cada novo dispositivo que tentar se conectar informando o ID.
    *   **Public (Público):** Permite o ingresso automático e a atribuição de IP para qualquer dispositivo que possua o Network ID, sem validação prévia.
*   **IPv4 Auto-Assign:** No subgrupo **Advanced**, selecione um escopo de endereçamento que utilize três blocos numéricos bem definidos na máscara (ex: `10.147.17.*`).

> [!warning] Atenção: Escopo de IPs Solitários
> Evite selecionar faixas de IP autoatribuídas simplificadas (com apenas dois blocos numéricos fixos), pois isso pode forçar a necessidade de configurar manualmente as faixas e IPs de cada cliente conectado à rede, invalidando o recurso de distribuição automática por DHCP virtual do ZeroTier.

# Instalação e Vínculo do Cliente no Servidor (Windows)
Para que a máquina que hospeda o serviço da API (Servidor local) distribua os dados na VPN, siga os passos abaixo:

1. No painel do ZeroTier, acesse a guia **Downloads** e baixe o instalador correspondente ao sistema operacional **Windows**.
2. Execute a instalação padrão. O aplicativo passará a ser executado em segundo plano, acessível através da bandeja do sistema (relógio do Windows).
3. Clique com o botão direito sobre o ícone do ZeroTier One e selecione **Join New Network**.
4. Insira o **Network ID** de 16 caracteres copiado do painel web e confirme.
5. O Windows exibirá um alerta de nova interface de rede localizada. Clique em **Sim** para autorizar o compartilhamento e a identificação na rede.

# Conexão e Homologação de Dispositivos Móveis (Android/iOS)
Para que os vendedores externos ou gestores consultem as informações a partir de smartphones:

1. Oriente o usuário a baixar o aplicativo oficial **ZeroTier One** na Google Play Store (Android) ou App Store (iOS).
2. Abra o aplicativo, clique em **Add Network** e insira o mesmo **Network ID** configurado no servidor.
3. Alterne a chave de ativação para a posição **Conectado/Ligado**.

### Homologação no Painel Web (Se a rede for Privada)
Se o controle de acesso foi configurado como **Private**, o dispositivo (computador ou celular) não trafegará dados imediatamente. 
1. Retorne ao painel web do ZeroTier e role a página até a seção **Members**.
2. Identifique o novo dispositivo conectado através do código identificador de hardware.
3. Preencha o campo **Short Name** com a identificação do proprietário (ex: `Notebook Lucas` ou `Celular Vendedor 01`).
4. Marque a caixa de seleção na coluna **Auth? (Authorize)**. O status mudará e a plataforma atribuirá dinamicamente o IP virtual baseado na faixa escolhida (ex: `10.147.17.5`).

# Validação de Acesso às APIs e Serviços
Após o servidor e os clientes móveis estarem autorizados e com os IPs gerados na mesma subnet virtual, os testes de validação podem ser executados.

### Descobrindo o IP Virtual da VPN no Servidor
* No painel do ZeroTier (seção Members), visualize o IP associado ao servidor.
* Alternativamente, no Windows, acesse o **Gerenciador de Redes e Compartilhamento**, localize a interface virtual criada pelo ZeroTier (ex: `Rede 8`) e verifique os detalhes do endereço IPv4 obtido.

### Testando os Serviços via Navegador / Aplicativo Externo
A partir de qualquer dispositivo conectado à VPN (mesmo fora da empresa), abra o navegador ou configure o aplicativo utilizando o IP Virtual seguido da porta padrão do serviço desejado:

```bash
# Exemplo de URL de acesso para o Servidor de Força de Vendas
[http://10.147.17.5:8082](http://10.147.17.5:8082)

# Exemplo de URL de acesso para o painel de Relatório Zap
[http://10.147.17.5:8077](http://10.147.17.5:8077)
````

Se as telas de login ou os dados de sincronização forem carregados com sucesso, a conectividade ponto a ponto está estabelecida de forma íntegra.

# Pontos Críticos e Regras de Segurança

> [!info] Persistência do Serviço
> 
> O ZeroTier é iniciado como um serviço nativo do sistema operacional. Portanto, o servidor manterá o mesmo IP virtual na VPN mesmo se a máquina for reiniciada ou a internet física sofrer quedas e oscilações, mantendo a configuração dos aplicativos móveis dos clientes perene.

> [!warning] Validação de Firewalls Locais
> 
> Caso os dispositivos móveis estejam conectados à VPN, mas não consigam abrir as URLs das APIs, o principal ponto de falha é o **Firewall do Windows** do servidor. Certifique-se de criar regras de entrada liberando o tráfego para as portas utilizadas pelos serviços do sistema (ex: `8082`, `8077`) para a sub-rede virtual do ZeroTier, impedindo o bloqueio local de conexões geradas pela interface virtual.

```
http://googleusercontent.com/youtube_content/1
```