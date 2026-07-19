---
id: [CASO-163]
link: https://www.youtube.com/watch?v=1GcQoYImK58
setor: [Implementação, Suporte, Infraestrutura]
modulo: [Configurações Gerais / White Label]
tags: [white-label, identidade-visual, personalizacao, executavel, customizacao, interface]
data_criacao: 2026-07-18
---

# Sumário
1. [[#Visão Geral do Conceito White Label]]
2. [[#Mapeamento de Arquivos de Imagem Estáticos (Diretório Raiz)]]
3. [[#Customização Avançada de Telas de Frente de Caixa (PDV / PDV Super)]]
4. [[#Parametrização das Strings Globais e Título da Aplicação]]
5. [[#Injeção de Paletas de Cores por Código (Cores de Splash)]]
6. [[#Modificação Estrutural do Ícone do Executável (Resource Hacker)]]
7. [[#Regras de Negócio e Pontos Críticos de Falha]]

# Visão Geral do Conceito White Label
A arquitetura de **White Label** do ERP permite que as empresas revendedoras (*Franquias / Parceiros comerciais*) ocultem em sua totalidade os registros de marca da desenvolvedora originária (`Código UP Sistemas`). O propósito é transferir à revenda a autonomia para comercializar e sustentar a ferramenta sob sua própria identidade corporativa, retendo e fidelizando sua carteira regional de clientes e protegendo o investimento aplicado em marketing e posicionamento de marca. 

O software foi projetado para ocultar referências nativas do código. A injeção da nova marca ocorre por substituição de ativos físicos em pasta ou edição de arquivos de inicialização, operando sem a necessidade de compilar novos executáveis na central.

# Mapeamento de Arquivos de Imagem Estáticos (Diretório Raiz)
O motor gráfico do ERP adota um comportamento de busca prioritária na raiz do seu diretório. Se determinados arquivos com nomenclaturas rígidas e extensões padronizadas estiverem presentes na mesma pasta do executável principal (`.exe`), o sistema substitui as telas de fábrica pelos ativos da revenda.

### Tabela de Ativos e Nomenclaturas Rígidas:
*   `carregando.png`: Imagem renderizada no centro da primeira tela de inicialização do sistema (Splash Screen de boot).
*   `login.png`: Imagem inserida na interface de autenticação do operador (sobreposta à janela de input de usuário e senha).
*   `logo.png`: Imagem expandida (escala maior) fixada no centro do painel gerencial/dashboard principal do ERP. É exibida durante a maior parte do tempo de uso administrativo.
*   `logo_pequena.png`: Imagem em dimensões compactadas fixada na barra de ferramentas superior ou nos cabeçalhos de menus colapsáveis.
*   `pdv.png`: Ativo de exibição de fundo na tela de vendas do operador. Atua como imagem padrão na grade lateral enquanto não há cupons abertos ou itens sendo bipados no leitor de código de barras.

> [!tip] Resolução e Formato dos Ativos
> Todos os arquivos listados devem obrigatoriamente seguir a extensão em letras minúsculas `.png` e contar com canal Alpha de transparência ativo para evitar recortes quadrados brancos ou distorções sobre o plano de fundo do sistema.

# Customização Avançada de Telas de Frente de Caixa (PDV / PDV Super)
As interfaces de faturamento veloz, [[PDV]] e `PDV Super`, possuem um painel específico de controle de estilo gráfico devido à alta exposição visual frente ao consumidor final no check-out.

1.  Acesse a tela de vendas do PDV.
2.  Logado com um usuário com privilégios de **Administrador**, clique no botão da engrenagem (Configurações).
3.  **Injeção de Fundo:** O painel disponibiliza um botão de upload para carregar um wallpaper personalizado que cobrirá todo o fundo da tela de vendas.
4.  **Ajustes de Fontes e Cores:** É possível mapear individualmente a cor de fundo e a cor da fonte de blocos de status, tais como o painel de `Caixa Livre`, `Caixa Fechado`, tabela de subtotal e janela de fechamento final de cupom.

```json
{
  "personalizacao_pdv_super": {
    "configuracao_estilo": "Habilitado",
    "controle_de_controles": {
      "visibilidade_botoes": "Customizável por operador",
      "exigir_senha_liberacao": "Parametrizável por rotina de atalho",
      "mapeamento_atalhos_teclado": "Permite redefinir chaves de funções (Ex: F5, F12)"
    }
  }
}