---
id: CASO-001
link: https://www.youtube.com/?hl=pt&gl=BR&app=desktop
setor: Suporte
modulo: Fiscal
tags: [nfce, offline, contingencia, sefaz]
data_criacao: 2026-07-18
---

# Sumário
- [[#Visão Geral]]
- [[#Configuração do Tipo de Emissão]]
- [[#Fluxo de Venda em Contingência Offline]]
- [[#Processo de Transmissão em Lote]]
- [[#Regras de Negócio e Validações]]

---

# Visão Geral

A emissão de [[NFC-e]] em modo **Offline** (Contingência) é um recurso legal que deve ser ativado exclusivamente quando houver impossibilidade técnica de comunicação com a [[SEFAZ]], seja por queda na conexão de internet do estabelecimento ou por instabilidade generalizada nos servidores do fisco.

> [!warning] Atenção
> A [[SEFAZ]] monitora a utilização do regime de contingência. O uso repetitivo, prolongado e sem justificativa válida deste recurso pode ser identificado como uma irregularidade, sujeitando o contribuinte ao **bloqueio da emissão** e à aplicação de **multas**. A transmissão síncrona/instantânea deve ser sempre a regra.

---

# Configuração do Tipo de Emissão

Para alternar o comportamento do sistema para o regime offline, o operador ou técnico deve realizar o ajuste diretamente nos parâmetros estruturais da empresa.

### Passo a Passo na Interface:
1. Acesse a tela de **Cadastro da Empresa**.
2. Localize a seção dedicada às configurações de **NFC-e**.
3. No campo **Tipo de Emissão**, altere o valor de **Normal** para **Offline**.
4. Salve as alterações para que as novas diretivas entrem em vigor no ponto de venda.

> [!tip] Dica
> O sistema possui um atalho na tela de gerenciamento de notas que redireciona o usuário diretamente para o **Cadastro da Empresa**, agilizando o retorno ao modo de emissão **Normal** assim que os serviços forem restabelecidos.

---

# Fluxo de Venda em Contingência Offline

Quando o sistema está parametrizado para o modo Offline, o comportamento da venda sofre modificações para garantir a continuidade da operação do estabelecimento:

1. **Finalização da Venda**: O operador realiza a venda normalmente no [[PDV]].
2. **Impressão do DANFE**: O sistema gera e imprime o documento fiscal para o cliente imediatamente.
3. **Alerta de Contingência**: A interface exibirá uma sinalização explícita informando que a nota foi emitida em modo contingência e que a consulta online na [[SEFAZ]] estará indisponível temporariamente.
4. **Status Interno**: No painel de gerenciamento, a nota assumirá o status de **Pendente sem confirmação** ou **Sem retorno**.

---

# Processo de Transmissão em Lote

As notas geradas em modo offline precisam ser obrigatoriamente transmitidas e autorizadas pela [[SEFAZ]] assim que a conexão for normalizada.

### Execução do Envio:
1. Acesse a tela de gerenciamento de notas fiscais.
2. Aplique o filtro para listar apenas as notas com o status **Não transmitidas**.
3. Selecione as notas desejadas utilizando as caixas de seleção.
4. Clique na seta ao lado do botão de transmissão e selecione a opção **Transmitir selecionadas**.
5. O sistema processará o envio em lote e atualizará o status de cada item com o retorno do servidor da [[SEFAZ]].

---

# Regras de Negócio e Validações

> [!info] Informação
> **Prazo Legal de Transmissão**: O contribuinte possui um prazo legal estrito para regularizar e transmitir as notas emitidas em contingência offline. O envio deve ocorrer **até o final do expediente do próximo dia útil** subsequente à emissão.

### Tratamento de Rejeições e Erros:
* Se uma nota enviada em lote apresentar alguma inconsistência de dados, a [[SEFAZ]] retornará um código de erro específico. O motivo da rejeição será exibido na coluna correspondente da interface.
* A nota permanecerá com o status **Sem confirmação** até que o erro seja corrigido e uma nova tentativa de transmissão obtenha sucesso.

> [!warning] Atenção
> **Proibição de Cancelamento e Inutilização**: Uma nota emitida offline em papel para o cliente **nunca** deve ser cancelada ou ter seu número inutilizado sem antes ser transmitida. Se o cliente tentar consultar a chave de acesso no portal do fisco e o documento não for encontrado por falta de envio, o estabelecimento poderá sofrer severas sanções fiscais. A numeração deve ser mantida, os erros corrigidos e a nota obrigatoriamente autorizada.

